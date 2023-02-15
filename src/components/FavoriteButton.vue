<script>
export default {
  name: "FavoriteButton",
  props: { text: String },
  data() {
    return {};
  },
  methods: {
    changeFavorite() {
      this.$emit("favoriteBtn");
    },
  },
  emits: ["favoriteBtn"],
};
</script>

<template>
  <button class="btn__favorite" @click="changeFavorite">{{ text }}</button>
</template>

<style scoped>
.btn__favorite {
  border-left: 2px solid dodgerblue;
  border-bottom: 2px solid dodgerblue;
  border-right: none;
  border-top: none;
  padding: 0.4rem 0.6rem;
  font-size: 2rem;
  background-color: azure;
}
</style>
