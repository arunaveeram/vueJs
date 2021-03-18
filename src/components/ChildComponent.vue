<template>
  <div id="app">
    <section v-if="errored">
      <p>
        We're sorry, we're not able to retrieve this information at the moment,
        please try back later
      </p>
    </section>

    <section v-else>
      <div v-if="loading">Loading...</div>

      <table style="width:100%">
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th>UserName</th>
          <th>Email</th>
        </tr>
        <tr v-for="user in users" :key="user.name">
          <th>{{ user.id }}</th>
          <th>{{ user.name }}</th>
          <th>{{ user.username }}</th>
          <th>{{ user.email }}</th>
        </tr>
      </table>
    </section>
  </div>
</template>

<script>
export default {
  name: 'ChildComponent',
  props: ['users'],
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
table,
th,
td {
  border: 1px solid black;
}
</style>
