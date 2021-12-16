<template>
  <span>
    <span class="ok" v-if="status == 'updated'" title="Enregistrement réalisé"
      ><i class="fas fa-check"></i
    ></span>
    <span
      class="working"
      v-else-if="status == 'update'"
      title="Enregistrement en cours"
      ><i class="fas fa-circle-notch fa-spin"></i
    ></span>
  </span>
</template>

<script>
export default {
  name: 'ActivityTag',
  props: ['status'],
  data() {
    return {};
  },
  mounted() {},
  methods: {},
};
</script>

<style scoped>
.ok,
.working {
  margin: 0.5em;
  padding: 0.1em;
}
.ok {
  color: #5fad41;
}
.working {
  color: #087e8b;
}
</style>
