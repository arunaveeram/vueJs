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
          v-on:removeUser="removeUser(index, id)"
        />
      </table>

      <button class="btn delete" v-on:click="addUser">
        ADD
      </button>
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
      newUser: [
        {
          id: 1,
          name: 'Leanne Graham',
          username: 'Bret',
          email: 'Sincere@april.biz',
        },
      ],
      msg: 'Welcome to my first Vue.js implementation',
      users: [],
      errored: false,
    };
  },
  beforeMount() {
    this.getUsers();
  },
  methods: {
    async addUser(newUser) {
      try {
        const newData = await axios.post(
          'https://jsonplaceholder.typicode.com/users/',
          newUser
        );
        console.log(newData);
        this.users.push({
          id: 11,
          name: 'Leanne Graham',
          username: 'Bret',
          email: 'Sincere@april.biz',
        });
      } catch (error) {
        console.log(error);
        this.errored = true;
      }
    },

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
        this.users.splice(index, 1);
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
