<template>
  <label class="checkbox">
    <input
      type="checkbox"
      :checked="valueC"
      :disabled="!enable"
      v-model="valueC"
      @change="saveOnChange"
    />
    {{ label }}
    <Activity-tag :status="status" />
  </label>
</template>

<script>
import ActivityTag from '../elements/ActivityTag.vue';
export default {
  name: 'Checkbox',
  props: ['label', 'enable', 'value', 'changeValue'],
  components: {
    ActivityTag,
  },
  data() {
    return {
      valueC: null,
      status: 'recorded',
    };
  },
  mounted() {
    this.valueC = this.value;
  },
  methods: {
    saveOnChange(e) {
      // propagation de la nouvelle valeur
      this.$emit('changeValue', this.valueC);

      // TODO faire appel api maj valeur

      // tag de mise à jour de la valeur
      this.status = 'update';
      setTimeout(() => {
        this.status = 'updated';
        setTimeout(() => {
          this.status = 'recorded';
        }, 1000);
      }, 4000);
    },
  },
};
</script>

<style scoped></style>
