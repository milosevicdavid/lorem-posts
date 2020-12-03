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

      <div v-if="query" class="card">
        <div class="card-wrapper">
          <span class="card-title"
            ><h1>{{ query.title }}</h1></span
          >
          <span class="card-body">{{ `${query.body}.` }}</span>
        </div>
      </div>
      <div class="post-holder" v-else>
        ... your selected post will display here
      </div>
    </div>
  </div>
</template>



<script>
import axios from "axios";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";

export default {
  data() {
    return {
      query: "",
      options: [],
    };
  },

  components: {
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
}

.post-holder {
  color: #69c28e;
  text-align: center;
  margin-top: 100px;
  font-size: 24px;
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

.subtitle {
  font-size: 11px;
  display: block;
  color: #299553;
}

.no-search {
  color: #fff;
}

.title {
  font-weight: 600;
  margin-top: 10px;
}

.subtitle {
  font-weight: 600;
  border-bottom: 1px solid #69c28e;
}

.card {
  display: flex;
  justify-content: center;
  align-items: center;

  &-wrapper {
    width: 50vw;
    margin-top: 50px;
  }

  &-title {
    display: block;
    text-transform: capitalize;
    background-color: #69c28e;
    padding: 20px;
    color: #fff;
    border-radius: 20px 20px 0 0;
  }

  &-body {
    display: block;
    background-color: #6fce96;
    padding: 20px;
    border-radius: 0 0 20px 20px;
    font-weight: 500;
    color: #fff;
    font-size: 16px;

    &::first-letter {
      text-transform: capitalize;
    }
  }
}
</style>
