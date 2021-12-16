<template>
  <div class="container is-fluid">
    <Breadcrumb :items="breadcrumbItems" />
    <h2 class="title">Dashboard</h2>
    <div class="notification is-warning" v-if="!updateMode">
      <strong>Modifications désactivées</strong>: Vous ne pouvez pas modifier
      les paramètres de cette page
    </div>
  </div>
</template>

<script>
import Breadcrumb from './elements/Breadcrumb.vue';
export default {
  name: 'PageDashboard',
  props: {},
  components: {
    Breadcrumb,
  },
  data() {
    return {
      breadcrumbItems: [{ text: 'Dashboard', href: '#', active: true }],
      updateMode: true,
    };
  },
  methods: {},
};
</script>

<style scoped></style>
