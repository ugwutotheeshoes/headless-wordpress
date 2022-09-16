<template>
  <div class="container">
    <p v-if="isLoading">Loading...</p>
    <ul v-for="p in post" :key="p.id">
      <h1>{{ p.title }}</h1>
      <p>{{ p.content }}</p>
      <p class="date">{{ p.createdAt }}</p>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      post: [],
      isLoading: false,
    };
  },
  methods: {
    getPosts() {
      this.isLoading = true;

      fetch("https://example.com/wp-json/wp/v2/posts")
        .then((response) => response.json())
        .then((data) => {
          this.post = data;
          this.isLoading = false;
        });
    },
  },
  mounted() {
    this.getPosts();
  },
};
</script>

<style>
html,
body {
  margin: 0;
  height: 100%;
  background-color: #fafafa;
  font-family: "Roboto", sans-serif;
}

body {
  margin-left: 15%;
  margin-right: 15%;
}
ul {
  margin-bottom: 10rem;
}
h1 {
  font-size: 3rem;
}
p {
  font-size: 1.8rem;
}
.container {
  padding-top: 60px;
}

.date {
  font-size: 1.2rem;
  display: flex;
  justify-content: end;
}
</style>
