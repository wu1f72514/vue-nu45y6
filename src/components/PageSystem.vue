<template>
  <div class="container is-fluid">
    <Breadcrumb :items="breadcrumbItems" v-if="displayMode == 'page'" />
    <h2 class="title">Système</h2>
    <div class="notification is-warning" v-if="!updateMode">
      <strong>Modifications désactivées</strong>: Vous ne pouvez pas modifier
      les paramètres de cette page
    </div>
    <div class="columns">
      <div class="column is-one-third">
        <Checkbox
          label="Mises à jour automatiques"
          :enable="updateMode"
          :value="xcUpdateAuto"
          @changeValue="changeValue('xcUpdateAuto', $event)"
        />
      </div>
      <div class="column is-one-third" v-if="xcUpdateAuto">
        <Text
          type="number"
          label="Sauvegardes toutes les"
          placeholder="1"
          maxlength="3"
          :enable="updateMode"
          :value="xtUpdateAutoIntervVal + ''"
          @changeValue="changeValue('xtUpdateAutoIntervVal', $event)"
        />
      </div>
      <div class="column" v-if="xcUpdateAuto">
        <Select
          label="Unité de fréquence"
          placeholder="Fréquence"
          :enable="updateMode"
          :values="xsUpdateAutoIntervUnityValues"
          :value="xsUpdateAutoIntervUnity"
          @changeValue="changeValue('xsUpdateAutoIntervUnity', $event)"
        />
      </div>
    </div>
    <div class="columns">
      <div class="column is-one-third">
        <Text
          label="Nom machine"
          placeholder="Mon_serveur"
          maxlength="25"
          :enable="updateMode"
          :value="xtHostname"
          @changeValue="changeValue('xtHostname', $event)"
        />
      </div>
      <div class="column is-one-third" v-if="xcUpdateAuto">
        <Text
          label="Système"
          maxlength="25"
          :readonly="true"
          :value="systemName"
        />
      </div>
      <div class="column" v-if="xcUpdateAuto">
        <Text label="Version" :readonly="true" :value="systemVersion" />
      </div>
    </div>
    <nav class="level">
      <div class="level-item has-text-centered">
        <div>
          <p class="heading">Uptime</p>
          <p class="title">{{ uptime.d }}j</p>
          <div class="buttons" style="margin-top: 10px">
            <button class="button is-warning is-small">Reboot</button>
            <button class="button is-danger is-small">Shutdown</button>
          </div>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="heading">Activité 1mn</p>
          <p class="title">{{ uptimeUsage1mn }}%</p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="heading">Activité 5mn</p>
          <p class="title">{{ uptimeUsage5mn }}%</p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="heading">Activité 15mn</p>
          <p class="title">{{ uptimeUsage15mn }}%</p>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import Breadcrumb from './elements/Breadcrumb.vue';
import Checkbox from './form/Checkbox.vue';
import Text from './form/Text.vue';
import Select from './form/Select.vue';
export default {
  name: 'PageSystem',
  props: {
    displayMode: {
      type: String,
      default: 'page',
    },
  },
  components: {
    Breadcrumb,
    Checkbox,
    Text,
    Select,
  },
  data() {
    return {
      breadcrumbItems: [
        { text: 'Dashboard', href: '#', active: false },
        { text: 'Paramétrage', href: '#', active: false },
        { text: 'Système', href: '#', active: true },
      ],
      xcUpdateAuto: true,
      xtUpdateAutoIntervVal: 1,
      xsUpdateAutoIntervUnity: 'w',
      xsUpdateAutoIntervUnityValues: [
        { label: 'an(s)', value: 'y' },
        { label: 'mois', value: 'm' },
        { label: 'semaine(s)', value: 'w' },
        { label: 'jour(s)', value: 'd' },
        { label: 'heure(s)', value: 'h' },
        { label: 'minute(s)', value: 'mn' },
        { label: 'seconde(s)', value: 's' },
      ],
      xtHostname: 'rpiHost',
      systemName: 'RaspberryOS',
      systemVersion: '1.0.5',
      systemDetails: 'Linux Infos',
      uptime: {
        d: 125,
        h: 23,
        mn: 59,
        s: 50,
      },
      uptimeText: null,
      uptimeUsage1mn: 10,
      uptimeUsage5mn: 100,
      uptimeUsage15mn: 58,
      updateMode: true,
    };
  },
  mounted() {
    // TODO load datas with api
  },
  methods: {
    changeValue: function (varN, value) {
      this[varN] = value;
    },
  },
};
</script>

<style scoped>
.center {
  text-align: center;
}
</style>
