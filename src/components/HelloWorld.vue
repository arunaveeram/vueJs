<template>
  <div class="app">
    <h1>{{ msg }}</h1>
    <section v-if="errored">
      <p>
        We're sorry, we're not able to retrieve this information at the moment,
        please try back later
      </p>
    </section>
    <section v-else>
      <table style="width:100%">
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th>UserName</th>
          <th>Email</th>
          <th>Delete user</th>
        </tr>
        <ChildComponent
          v-for="(user, index) in users"
          :key="index"
          :name="user.name"
          :id="user.id"
          :username="user.username"
          :email="user.email"
          v-on:removeUser="removeUser"
        />
      </table>
    </section>
  </div>
</template>

<script>
import ChildComponent from './ChildComponent.vue';
import axios from 'axios';
export default {
  name: 'HelloWorld',
  components: {
    ChildComponent,
  },
  data() {
    return {
      msg: 'Welcome to my first Vue.js implementation',
      users: [],
      errored: false,
    };
  },
  beforeMount() {
    this.getUsers();
  },
  methods: {
    async getUsers() {
      try {
        const { data } = await axios.get(
          'https://jsonplaceholder.typicode.com/users'
        );
        this.users = data;
      } catch (error) {
        console.log(error);
        this.errored = true;
      }
    },
    async removeUser(index) {
      try {
        const result = await axios.delete(
          'https://jsonplaceholder.typicode.com/users/${id}'
        );
        console.log(result);
        if (result.status === 200) {
          this.users.splice(index + 1, 1);
        } else {
          console.log(result);
        }
      } catch (error) {
        console.log(error);
        this.errored = true;
      }
    },
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
