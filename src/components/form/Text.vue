<template>
  <div class="field">
    <label class="label" :for="idGen" v-if="label !== ''">{{ label }}</label>
    <div class="control">
      <input
        class="input"
        :type="type"
        :placeholder="placeholder"
        :readonly="readonly"
        :maxlength="maxlength"
        :id="idGen"
        v-model="valueC"
        :disabled="!enable"
        @change="saveOnChange"
      />
    </div>
    <Activity-tag :status="status" v-if="activityTag" />
  </div>
</template>

<script>
import ActivityTag from '../elements/ActivityTag.vue';
export default {
  name: 'Text',
  props: {
    type: {
      type: String,
      default: 'text',
    },
    label: {
      type: String,
      default: '',
    },
    placeholder: {
      type: String,
      default: '',
    },
    maxlength: {
      type: String,
      default: null,
    },
    enable: {
      type: Boolean,
      default: true,
    },
    readonly: {
      type: Boolean,
      default: false,
    },
    value: {
      type: String,
      default: '',
    },
    activityTag: {
      type: Boolean,
      default: true,
    },
    changeValue: {
      type: Object,
      default: null,
    },
  },
  components: {
    ActivityTag,
  },
  data() {
    return {
      valueC: null,
      idGen: null,
      status: 'recorded',
      pxPerChar: 17,
      mPx: 1,
    };
  },
  mounted() {
    this.valueC = this.value;
    this.idGen = this.randomChars();
    this.mPx = this.maxlength ? this.maxlength : 10;
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
    randomChars(length = 15) {
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
input:read-only {
  border: 0px solid transparent;
  cursor: default;
}
</style>
