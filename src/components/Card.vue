<template>
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
</template>

<script>
export default {
  props: ["query"],
};
</script>

<style lang="scss">
.post-holder {
  color: #69c28e;
  text-align: center;
  margin-top: 100px;
  font-size: 24px;
}

.card {
  display: flex;
  justify-content: center;
  align-items: center;

  &-wrapper {
    width: 50vw;
    margin-top: 50px;

    @media (max-width: 576px) {
      width: 80vw;
    }
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
