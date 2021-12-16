<template>
  <div class="container is-fluid">
    <section class="hero">
      <div class="hero-body">
        <p class="title">404</p>
        <p class="subtitle">Page demandée non-trouvée !</p>
      </div>
    </section>
    <div class="buttons">
      <button class="button is-primary" @click="passEvent_changePage">
        Retour
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Page404',
  props: {
    browserHistory: {
      type: Array,
      default: [],
    },
  },
  components: {},
  data() {
    return {};
  },
  methods: {
    passEvent_changePage() {
      this.$emit(
        'changePage',
        this.browserHistory[this.browserHistory.length - 2].page
      );
    },
  },
};
</script>

<style scoped></style>
