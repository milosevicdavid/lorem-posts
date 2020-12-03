<template>
  <div class="container">
    <div class="wrapper">
      <v-select
        class="style-chooser"
        v-model="query"
        label="title"
        :clearable="false"
        :options="options"
        placeholder="Please start entering text to search"
      >
        <template v-slot:option="option">
          <div class="title">
            {{ option.title }}
          </div>
          <div class="subtitle">
            {{ `${option.body.slice(0, 40)} ...` }}
          </div>
        </template>
        <template v-slot:no-options="{ search, searching }">
          <template v-if="searching">
            <PulseLoader />
          </template>
          <template v-if="searching">
            <span class="no-search">
              Sorry, we couldn't find anything :(
            </span>
          </template>
        </template>
      </v-select>

      <Card :query="query" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Card from "./components/Card.vue";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";

export default {
  data() {
    return {
      options: [],
      query: ""
    };
  },

  components: {
    Card,
    PulseLoader,
  },

  mounted: function() {
    return axios
      .get("https://jsonplaceholder.typicode.com/posts?q=lorem")
      .then((res) => {
        this.options = res.data;
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

.style-chooser {
  .vs__dropdown-toggle {
    color: #394066;
    font-size: 14px;
    height: 44px;
    border-radius: 8px;
  }

  .vs__search::placeholder {
    opacity: 0.5;
    content: "";
  }

  .vs__dropdown-menu {
    background-color: #6fce96;
    border-radius: 0 0 20px 20px;
  }

  li {
    background-color: #6fce96;
    color: white;
    text-transform: capitalize;

   
    &:hover {
      background-color: #69c28e;
      color: white;
    }
  }

  .vs__clear,
  .vs__open-indicator {
    fill: #394066;
  }
}

.title {
  font-weight: 600;
  margin-top: 10px;

}

.subtitle {
  font-size: 11px;
  display: block;
  color: #299553;
  font-weight: 600;
  border-bottom: 1px solid #69c28e;
}

.no-search {
  color: #fff;
}


</style>
