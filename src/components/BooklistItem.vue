<script>
import FavoriteButton from "../components/FavoriteButton.vue";
export default {
  components: { FavoriteButton },
  name: "BooklistItem",
  props: {
    book: Object,
    favorites: Array,
  },
  data() {
    return {
      content: "🤍",
    };
  },
  methods: {
    setFavorite() {
      if (this.content === "🤍") {
        this.content = "❤️";
        this.book.favorite = true;
        this.favorites.push(this.book.id);
      } else {
        this.content = "🤍";
        this.book.favorite = false;
        let bookIndex = this.favorites.indexOf(this.book.id);
        this.favorites.splice(bookIndex, 1);
      }

      localStorage.setItem("safeFavorites", JSON.stringify(this.favorites));
    },
    showFavorite() {
      if (this.favorites.includes(this.book.id)) {
        this.content = "❤️";
      }
    },
  },
  beforeUpdate() {
    this.showFavorite();
  },
};
</script>

<template>
  <li class="booklist__item">
    <FavoriteButton
      class="btn__style"
      @favoriteBtn="setFavorite()"
      :text="content"
    />
    <img :src="book.cover" alt="Coverbild" class="booklist__item--image" />
    <div>
      <p class="booklist__item--author">{{ book.author }}</p>
      <p class="booklist__item--title">{{ book.title }}</p>
      <p class="booklist__item--isbn">{{ book.price }}</p>
      <p>{{ book.favorite }}</p>
    </div>
  </li>
</template>

<style scoped>
.booklist__item {
  list-style: none;
  border: 2px solid dodgerblue;
  display: flex;
  justify-content: space-around;
  align-items: center;
  gap: 1rem;
  background-color: white;
  width: 85vw;
  padding-right: 1rem;
  position: relative;
}
.booklist__item--title {
  font-weight: bold;
}
.booklist__item--author,
.booklist__item--price {
  font-size: 1.3rem;
}
.booklist__item--author {
  padding-top: 2rem;
  padding-right: 3rem;
}
.booklist__item--image {
  width: 10rem;
  height: 15rem;
}
.btn__style {
  position: absolute;
  top: 0;
  right: 0;
}
</style>
