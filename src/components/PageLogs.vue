<template>
  <div class="container is-fluid">
    <Breadcrumb :items="breadcrumbItems" />
    <h2 class="title">Logs</h2>
    <div class="columns">
      <div class="column">
        <Select
          label="Date"
          placeholder="Filtrer par date"
          :values="filterDates"
          :value="filterChoiceDate"
          @changeValue="changeValue('filterChoiceDate', $event)"
        />
      </div>
      <div class="column">
        <Select
          label="Domaines"
          placeholder="Filtrer par domaine"
          :values="filterDomains"
          :value="filterChoiceDomain"
          @changeValue="changeValue('filterChoiceDomain', $event)"
        />
      </div>
      <div class="column">
        <Select
          label="Gravité"
          placeholder="Filtrer par gravité"
          :values="filterGravities"
          :value="filterChoiceGravity"
          @changeValue="changeValue('filterChoiceGravity', $event)"
        />
      </div>
    </div>
    {{ logs }}
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
        <tr
          v-for="log in logs"
          :class="log.gravity.toLowerCase()"
          :style="!log.visible ? 'display:none;' : ''"
        >
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
import Select from './form/Select.vue';
export default {
  name: 'pageLogs',
  props: {},
  components: {
    Breadcrumb,
    Select,
  },
  data() {
    return {
      breadcrumbItems: [
        { text: 'Dashboard', href: '#', active: false },
        { text: 'Logs', href: '#logs', active: true },
      ],
      updateMode: true,
      filterDates: [],
      filterChoiceDate: null,
      filterDomains: [],
      filterChoiceDomain: null,
      filterGravities: [],
      filterChoiceGravity: null,
      filterChoiceMessage: null,
      logs: [
        {
          datetime: '2021-01-02 12:34:56.789012',
          domain: 'Apache',
          gravity: 'critical',
          score: 14,
          message: 'Lorem ipsum',
          visible: true,
        },
        {
          datetime: '2019-03-01 00:00:00.000000',
          domain: 'Apache',
          gravity: 'error',
          score: 14,
          message: 'Lorem ipsum',
          visible: true,
        },
        {
          datetime: '2019-03-01 00:00:00.000000',
          domain: 'Apache',
          gravity: 'warning',
          score: 14,
          message: 'Lorem ipsum',
          visible: true,
        },
        {
          datetime: '2019-03-01 00:00:00.000000',
          domain: 'Nginx',
          gravity: 'info',
          score: 14,
          message: 'Lorem ipsum',
          visible: true,
        },
        {
          datetime: '2019-01-01 00:00:00.000000',
          domain: 'Apache',
          gravity: 'notice',
          score: 14,
          message: 'Lorem ipsum',
          visible: true,
        },
      ],
    };
  },
  mounted() {
    let existsDates = [];
    let existsDomains = [];
    let existsGravities = [];
    this.logs.forEach((logMsg) => {
      // date
      let d = logMsg.datetime.substr(0, 10);
      if (existsDates.indexOf(d) == -1) {
        this.filterDates.push({ value: d, label: d });
        existsDates.push(d);
      }
      // domaines
      if (existsDomains.indexOf(logMsg.domain) == -1) {
        this.filterDomains.push({ value: logMsg.domain, label: logMsg.domain });
        existsDomains.push(logMsg.domain);
      }
      // gravités
      if (existsGravities.indexOf(logMsg.gravity) == -1) {
        this.filterGravities.push({
          value: logMsg.gravity,
          label: logMsg.gravity,
        });
        existsGravities.push(logMsg.domain);
      }
    });
  },
  methods: {
    fmtDatetime(datetime, format = 'd/m/Y h:i') {
      let w = datetime.split(' ');
      let w2 = w[0].split('-');
      let w3 = w[1].split('.');
      let w4 = w3[0].split(':');
      let y = w2[0];
      let m = w2[1];
      let d = w2[2];
      let h = w4[0];
      let mn = w4[1];
      let s = w4[2];
      let ms = w3[1];
      if (format == 'd/m/Y h:i:s ms') {
        return (
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            d * 1
          ) +
          '/' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            m * 1
          ) +
          '/' +
          y +
          ' ' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            h * 1
          ) +
          ':' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            mn * 1
          ) +
          ':' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            s * 1
          ) +
          ' ' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 6 }).format(
            ms * 1
          )
        );
      } else if (format == 'd/m/Y h:i') {
        return (
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            d * 1
          ) +
          '/' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            m * 1
          ) +
          '/' +
          y +
          ' ' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            h*1
          ) +
          ':' +
          new Intl.NumberFormat('fr-FR', { minimumIntegerDigits: 2 }).format(
            mn*1
          )
        );
      }
    },
    applyLogFilters() {
      this.logs.forEach((log) => {
        // date
        if (this.filterChoiceDate !== null && this.filterChoiceDate !== '') {
          if (log.datetime.substr(0, 10) != this.filterChoiceDate) {
            log.visible = false;
            return;
          }
        }
        // gravité
        if (
          this.filterChoiceGravity !== null &&
          this.filterChoiceGravity !== ''
        ) {
          if (log.gravity != this.filterChoiceGravity) {
            log.visible = false;
            return;
          }
        }

        log.visible = true;
      });
    },
    changeValue: function (varN, value) {
      this[varN] = value;
      this.applyLogFilters();
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
