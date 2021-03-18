<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <ChildComponent v-bind:users="users" />
  </div>
</template>

<script>
import ChildComponent from './ChildComponent.vue';
import axios from 'axios';
export default {
  components: {
    ChildComponent,
  },
  data() {
    return {
      users: [],
      loading: true,
      errored: false,
    };
  },

  mounted() {
    axios
      .get('https://jsonplaceholder.typicode.com/users')
      .then((response) => {
        this.users = response.data;
        console.log('info', this.users);
      })
      .catch((error) => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
</style>
