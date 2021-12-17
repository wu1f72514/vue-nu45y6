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
          <td :title="fmtDatetime(log.datetime, 'd/m/Y h:i:s ms')">
            {{ fmtDatetime(log.datetime) }}
          </td>
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
      filterDates: [],
      filterChoiceDates: null,
      filterDomains: [],
      filterChoiceDomains: null,
      filterGravities: [],
      filterChoiceGravities: null,
      filterChoiceMessages: null,
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
          domain: 'Nginx',
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
  methods: {
    fmtDatetime(datetime, format = 'd/m/Y h:i') {
      let d = new Date(datetime);
      if (format == 'd/m/Y h:i:s ms') {
        return (
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            d.getDay()
          ) +
          '/' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            d.getMonth() + 1
          ) +
          '/' +
          d.getFullYear() +
          ' ' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            d.getHours()
          ) +
          ':' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            d.getMinutes()
          ) +
          ':' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            d.getSeconds()
          ) +
          ' ' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 6 }).format(
            d.getMilliseconds()
          )
        );
      } else if (format == 'd/m/Y h:i') {
        return (
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            d.getDay()
          ) +
          '/' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            d.getMonth() + 1
          ) +
          '/' +
          d.getFullYear() +
          ' ' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            d.getHours()
          ) +
          ':' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            d.getMinutes()
          )
        );
      }
    },
  },
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
