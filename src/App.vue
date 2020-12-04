<template>
  <div class="container">
    <div class="wrapper">
      <Search :options="fetchedOptions" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Search from "./components/Search.vue"

export default {
  data() {
    return {
      fetchedOptions: [],
    };
  },

  components: {
    Search
  },

  mounted: function() {
    return axios
      .get("https://jsonplaceholder.typicode.com/posts?q=lorem")
      .then((res) => {
        this.fetchedOptions = res.data;
      });
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Varela+Round&display=swap");

body {
  background-color: rgb(171, 251, 146, 0.4);
  font-family: "Varela Round", sans-serif;
}

.container {
  margin-top: 100px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.wrapper {
  width: 65vw;

  @media (max-width: 576px) {
    width: 90vw;
  }
}

</style>
