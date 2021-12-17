<template>
  <nav class="pagination is-centered" role="navigation" aria-label="pagination">
    <a class="pagination-previous" :data-page="1" @click="changePageClick"
      ><i class="fas fa-angle-double-left" :data-page="1"></i
    ></a>
    <a class="pagination-next" :data-page="nbPages" @click="changePageClick"
      ><i class="fas fa-angle-double-right" :data-page="nbPages"></i
    ></a>
    <ul class="pagination-list">
      <li v-for="i in nbPages">
        <a
          :class="'pagination-link' + (pageC == i ? ' is-current' : '')"
          :key="i"
          :title="'Aller à la page ' + i"
          :aria-label="'Aller à la page ' + i"
          :data-page="i"
          @click="changePageClick"
          v-if="
            manageCesure === false ||
            startMiddleGroup === null ||
            (i * 1 > startMiddleGroup && i * 1 < startMiddleGroup * 2 - 1) ||
            i * 1 === 1 ||
            i * 1 === nbPages * 1
          "
          >{{ i }}
        </a>
        <span
          class="pagination-ellipsis"
          v-else-if="
            startMiddleGroup !== null &&
            (i == startMiddleGroup - 1 || i == nbPages - 2)
          "
          >&hellip;</span
        >
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'Pagination',
  props: {
    page: {
      type: Number,
      default: 1,
    },
    nbPages: {
      type: Number,
      default: 99,
    },
    changeValue: {
      type: Object,
      default: null,
    },
    manageCesure: {
      type: Boolean,
      default: true,
    },
  },
  components: {},
  data() {
    return {
      pageC: null,
      nbSliceMiddleShown: 5,
      startMiddleGroup: null,
    };
  },
  mounted() {
    // TODO qd changement de page changer la composition des chiffres cliquables
    this.pageC = this.page;
    if (this.manageCesure && this.nbPages >= this.nbSliceMiddleShown * 2) {
      this.startMiddleGroup = Math.floor(
        (this.nbPages - this.nbSliceMiddleShown) / 2
      );
    }
  },
  methods: {
    changePageClick(e) {
      this.pageC = e.target.dataset.page;

      // propagation de la nouvelle valeur
      this.$emit('changePage', this.pageC);
    },
  },
};
</script>

<style scoped></style>
