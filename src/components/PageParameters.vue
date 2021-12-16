<template>
  <div class="container is-fluid">
    <Breadcrumb :items="breadcrumbItems" />
    <h2 class="title">Paramétrage</h2>
    <div class="notification is-warning" v-if="!updateMode">
      <strong>Modifications désactivées</strong>: Vous ne pouvez pas modifier
      les paramètres de cette page
    </div>
    <div class="box"><Page-system displayMode="incrust" /></div>
  </div>
</template>

<script>
import Breadcrumb from './elements/Breadcrumb.vue';
import PageSystem from './PageSystem.vue';
export default {
  name: 'PageParameters',
  props: [],
  components: {
    Breadcrumb,
    PageSystem,
  },
  data() {
    return {
      breadcrumbItems: [
        { text: 'Dashboard', href: '#', active: false },
        { text: 'Paramétrage', href: '#', active: true },
      ],
      updateMode: true,
    };
  },
  methods: {},
};
</script>

<style scoped></style>
