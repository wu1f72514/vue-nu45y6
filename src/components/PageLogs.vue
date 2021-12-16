<template>
  <div class="container is-fluid">
    <Breadcrumb :items="breadcrumbItems" />
    <h2 class="title">Logs</h2>
  </div>
</template>

<script>
import Breadcrumb from './elements/Breadcrumb.vue';
export default {
  name: 'pageLogs',
  props: {},
  components: {
    Breadcrumb,
  },
  data() {
    return {
      breadcrumbItems: [
        { text: 'Dashboard', href: '#', active: false },
        { text: 'Logs', href: '#logs', active: true },
      ],
      updateMode: true,
    };
  },
  methods: {},
};
</script>

<style scoped></style>
