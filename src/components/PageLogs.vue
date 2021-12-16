<template>
  <div class="container is-fluid">
    <Breadcrumb :items="breadcrumbItems" />
    <h2 class="title">Logs</h2>
    <table class="table">
      <thead>
        <tr>
          <th>Date</th>
          <th>Domaine</th>
          <th>Gravité</th>
          <th>Score</th>
          <th>Message</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="log in logs">
          <td>{{ log.datetime }}</td>
          <td>{{ log.domain }}</td>
          <td>{{ log.gravity }}</td>
          <td>{{ log.score }}</td>
          <td>{{ log.message }}</td>
        </tr>
      </tbody>
    </table>
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
      logs: [
        {
          datetime: '2019-01-01T00:00:00.000Z',
          domain: 'Apache',
          gravity: 'error',
          score: 14,
          message: 'Lorem ipsum',
        },
      ],
    };
  },
  methods: {},
};
</script>

<style scoped>
.notice {
  color: #5fad41;
}
.critical {
  color: brown;
}
.error {
  color: red;
}
.warning {
  color: ornage;
}
.info {
  color: #087e8b;
}
</style>
