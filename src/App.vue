<template>
  <div id="container">
    <v-select
      class="style-chooser"
      v-model="query"
      label="title"
      :clearable="false"
      :options="options"
      placeholder="Please start entering text to search"
    >
    </v-select>
    <div>
      {{ query.title }} <br />
      {{ query.body }}
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      query: "",
      options: [],
    };
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
.style-chooser {
  .vs__search::placeholder,
  .vs__dropdown-toggle {
    color: #394066;
    font-size: 14px;
    height: 44px;
    border-radius: 8px;
  }

  .vs__dropdown-menu {
    background-color: #6fce96;
    border-radius: 0 0 20px 20px;
  }

  li:hover {
    background-color: #69c28e;
    color: white;
  }

  li {
    background-color: #6fce96;
    color: white;
    text-transform: capitalize;
  }

  .vs__clear,
  .vs__open-indicator {
    fill: #394066;
  }
}
</style>
