<template>
  <nav class="breadcrumb is-right" aria-label="breadcrumbs">
    <ul>
      <li v-for="item in items" :class="item.active ? 'is-active' : ''">
        <a :href="item.href">{{ item.text }}</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'Text',
  props: {
    items: {
      type: Array,
      default: [],
    },
  },
  components: {},
  data() {
    return {};
  },
  mounted() {},
  methods: {},
};
</script>

<style scoped></style>
