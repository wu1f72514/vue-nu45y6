<template>
  <div id="app">
    <section class="section">
      <div class="container">
        <Nav-bar @changePage="changePage($event)" />
        <PageParameters v-if="pageDisplayed == 'parameters'" />
        <PageSystem v-else-if="pageDisplayed == 'system'" />
        <PageLogs v-else-if="pageDisplayed == 'logs'" />
        <PageDashboard v-else-if="pageDisplayed == 'home'" />
        <Page404
          v-else
          :browserHistory="browserHistory"
          @changePage="changePage($event)"
        />
      </div>
    </section>
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue';
import PageParameters from './components/PageParameters.vue';
import PageSystem from './components/PageSystem.vue';
import PageDashboard from './components/PageDashboard.vue';
import PageLogs from './components/PageLogs.vue';
import Page404 from './components/Page404.vue';

const existsPages = ['parameters', 'system', 'home', 'logs'];
export default {
  name: 'App',
  components: {
    NavBar,
    PageParameters,
    PageSystem,
    PageDashboard,
    PageLogs,
    Page404,
  },
  data() {
    return {
      pageDisplayed: null,
      browserHistory: [],
    };
  },
  methods: {
    changePage: function (page) {
      this.pageDisplayed = page;

      // mémoriser le parcours utilisateur
      this.browserHistory.push({
        page: page,
        result: existsPages.indexOf(page),
        time: new Date(),
      });
    },
  },
};
// TODO stcoker dans le browser et/ou remonter à une api le parcours utilisateur pour stats
</script>

<style>
.title {
  font-size: 1.2em;
}
</style>
