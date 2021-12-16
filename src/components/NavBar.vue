<template>
  <nav class="navbar is-transparent">
    <div class="navbar-brand">
      <a
        class="navbar-item"
        :href="nav[0].href"
        :target="nav[0].target"
        @click="passEvent_changePage"
      >
        App
      </a>
      <div class="navbar-burger" data-target="navbarExampleTransparentExample">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>

    <div id="navbarExampleTransparentExample" class="navbar-menu">
      <div class="navbar-start">
        <template v-for="navItem in nav">
          <a
            class="navbar-item"
            :href="navItem.href"
            :target="navItem.target"
            @click="passEvent_changePage"
            v-if="navItem.children.length == 0"
          >
            {{ navItem.text }}
          </a>
          <div class="navbar-item has-dropdown is-hoverable" v-else>
            <a
              class="navbar-link"
              :href="navItem.href"
              :target="navItem.target"
              @click="passEvent_changePage"
            >
              {{ navItem.text }}
            </a>
            <div class="navbar-dropdown is-boxed">
              <template v-for="child in navItem.children">
                <a
                  class="navbar-item"
                  :href="child.href"
                  :target="child.target"
                  @click="passEvent_changePage"
                >
                  {{ child.text }}
                </a>
              </template>
            </div>
          </div>
        </template>
      </div>

      <div class="navbar-end"></div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'NavBar',
  props: [],
  data() {
    return {
      nav: [
        {
          text: 'Accueil',
          href: '#home',
          target: '_self',
          children: [],
        },
        {
          text: 'Paramétrage',
          href: '#parameters',
          target: '_self',
          children: [
            {
              text: 'Système',
              href: '#system',
              target: '_self',
              children: [],
            },
            {
              text: 'Serveurs pairs',
              href: '#peers',
              target: '_self',
              children: [],
            },
            {
              text: 'Données',
              href: '#datas',
              target: '_self',
              children: [],
            },
          ],
        },
        {
          text: 'Logs',
          href: '#logs',
          target: '_self',
          children: [],
        },
      ],
    };
  },
  methods: {
    passEvent_changePage(e) {
      let w = e.target.href.split('#');
      this.$emit('changePage', w[w.length - 1]);
    },
  },
};
</script>

<style scoped></style>
