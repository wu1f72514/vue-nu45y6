<template>
  <div class="container is-fluid">
    <Breadcrumb :items="breadcrumbItems" />
    <h2 class="title">Logs</h2>
    <table class="table">
      <thead>
        <tr>
          <th></th>
          <th>Date</th>
          <th>Domaine</th>
          <th>Gravité</th>
          <th>Score</th>
          <th>Message</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="log in logs" :class="log.gravity.toLowerCase()">
          <td>
            <i class="fas fa-times" v-if="log.gravity == 'error'"></i>
            <i
              class="fas fa-exclamation-triangle"
              v-else-if="log.gravity == 'warning'"
            ></i>
            <i class="fas fa-info-circle" v-else-if="log.gravity == 'info'"></i>
            <i class="fas fa-flag" v-else-if="log.gravity == 'notice'"></i>
            <i class="fas fa-poop" v-else-if="log.gravity == 'critical'"></i>
          </td>
          <td>{{ log.datetime }}</td>
          <td>{{ log.domain }}</td>
          <td>
            <strong :class="log.gravity.toLowerCase()">{{
              log.gravity.toUpperCase()
            }}</strong>
          </td>
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
          gravity: 'critical',
          score: 14,
          message: 'Lorem ipsum',
        },
        {
          datetime: '2019-01-01T00:00:00.000Z',
          domain: 'Apache',
          gravity: 'error',
          score: 14,
          message: 'Lorem ipsum',
        },
        {
          datetime: '2019-01-01T00:00:00.000Z',
          domain: 'Apache',
          gravity: 'warning',
          score: 14,
          message: 'Lorem ipsum',
        },
        {
          datetime: '2019-01-01T00:00:00.000Z',
          domain: 'Apache',
          gravity: 'info',
          score: 14,
          message: 'Lorem ipsum',
        },
        {
          datetime: '2019-01-01T00:00:00.000Z',
          domain: 'Apache',
          gravity: 'notice',
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
  color: orange;
}
.info {
  color: #087e8b;
}
</style>
