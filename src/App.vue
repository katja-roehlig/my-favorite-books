<script>
import BooklistItem from "./components/BooklistItem.vue";
export default {
  components: { BooklistItem },
  data() {
    return {
      bookData: [],
      favorites: [],
    };
  },
  methods: {
    async getBooks() {
      const response = await fetch("http://localhost:4730/books?_limit=12/");
      this.bookData = await response.json();
    },
    async getState() {
      this.favorites = JSON.parse(localStorage.getItem("safeFavorites")) || [];

      for (let i = 0; i < this.bookData.length; i++) {
        this.bookData[i].favorite = this.favorites.includes(
          this.bookData[i].id
        );
        /* if (this.bookData[i]) {
          console.log("Juhuu");
          this.content = "❤️";
        } */
      }
    },
  },
  async created() {
    await this.getBooks();
    await this.getState();
  },
};
</script>

<template>
  <main>
    <ul class="booklist__container">
      <BooklistItem
        v-for="book of bookData"
        :key="book.id"
        :book="book"
        :favorites="favorites"
      />
    </ul>
  </main>
</template>

<style scoped>
main {
  background-color: pink;
}
.booklist__container {
  padding: 2rem 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 2rem;
}
</style>
