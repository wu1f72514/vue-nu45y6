<template>
  <div class="field">
    <label class="label" :for="idGen" v-if="label !== ''">{{ label }}</label>
    <div class="control">
      <div class="select">
        <select
          v-model="valueC"
          :id="idGen"
          :disabled="!enable"
          @change="saveOnChange"
        >
          <option
            v-for="value in values"
            :value="value.value"
            :selected="valueC == value.value"
          >
            {{ value.label }}
          </option>
        </select>
      </div>
    </div>
    <Activity-tag :status="status" />
  </div>
</template>

<script>
import ActivityTag from '../elements/ActivityTag.vue';
export default {
  name: 'Select',
  props: ['label', 'placeholder', 'enable', 'values', 'value', 'changeValue'],
  components: {
    ActivityTag,
  },
  data() {
    return {
      valueC: null,
      idGen: null,
      status: 'recorded',
    };
  },
  mounted() {
    this.valueC = this.value;
    this.idGen = this.makeid();
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
    makeid(length = 15) {
      let result = '';
      const characters =
        'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789_';
      for (var i = 0; i < length; i++) {
        result += characters.charAt(
          Math.floor(Math.random() * characters.length)
        );
      }
      return result;
    },
  },
};
</script>

<style scoped>
select {
  margin-left: 1em;
}
</style>
