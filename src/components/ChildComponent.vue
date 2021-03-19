<template>
  <tr>
    <th>{{ id }}</th>
    <th>{{ name }}</th>
    <th>{{ username }}</th>
    <th>{{ email }}</th>
    <th>
      <button class="btn delete" v-on:click="removeChild">
        Delete
      </button>
    </th>
  </tr>
</template>

<script>
export default {
  name: 'ChildComponent',
  props: ['name', 'id', 'username', 'email'],
  methods: {
    removeChild() {
      this.$emit('removeUser', this.key + 1);
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
table,
th,
td {
  border: 1px solid black;
}
</style>
