<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <Joke
      v-for="joke in jokes"
      :key="joke.id"
      :id="joke.id"
      :joke="joke.joke"
    />
  </div>
</template>

<script>
import axios from "axios";
import Joke from "../../components/Joke.vue";
import SearchJokes from "../../components/searchJokes";

export default {
  components: {
    Joke,
    SearchJokes,
  },
  data() {
    return {
      jokes: [],
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json",
      },
    };

    try {
      const res = await axios.get("https://icanhazdadjoke.com/search", config);
      // console.log(res);
      this.jokes = res.data.results;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    async searchText(text) {
      const config = {
        headers: {
          Accept: "application/json",
        },
      };

      try {
        const res = await axios.get(
          `https://icanhazdadjoke.com/search?term=${text}`,
          config
        );
        // console.log(res);
        this.jokes = res.data.results;
      } catch (error) {
        console.log(error);
      }
    },
  },
  head() {
    return {
      title: "The Jokes of Dad",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Best place for dumb jokes",
        },
      ],
    };
  },
};
</script>

<style>
</style>