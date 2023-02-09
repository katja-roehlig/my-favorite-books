<script>
export default {
  data() {
    return {
      bookData: [],
    };
  },
  methods: {
    async getBooks() {
      const response = await fetch("http://localhost:4730/books?_limit=12/");
      this.bookData = await response.json();
    },
  },
  async created() {
    this.getBooks();
  },
};

//import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <main>
    <ul class="booklist__container">
      <li class="booklist__item" v-for="book in bookData" :key="book.id">
        <img :src="book.cover" alt="Coverbild" class="booklist__item--image" />
        <div>
          <p class="booklist__item--author">{{ book.author }}</p>
          <p class="booklist__item--title">{{ book.title }}</p>
          <p class="booklist__item--isbn">{{ book.isbn }}</p>
        </div>
      </li>
    </ul>
  </main>
</template>

<style scoped>
main {
  background-color: pink;
  display: flex;
}
.booklist__container {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
}
.booklist__item {
  list-style: none;
  border: 2px solid dodgerblue;
  width: 27vw;
  display: flex;
  justify-content: space-around;
  align-items: center;
  background-color: white;
}
.booklist__item--title {
  font-weight: bold;
}
.booklist__item--author,
.booklist__item--isbng {
  font-size: 1.3rem;
}
.booklist__item--image {
  width: 10rem;
  height: 15rem;
}
</style>
