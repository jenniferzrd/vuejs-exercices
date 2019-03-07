<template>
  <div class="about">
    <h1 class="text-capitalize blue--text">users list</h1>
      <ul>
      <li v-for="user in users" :key="user.id">
        <!-- <div v-if="edit === user.id">
          <input type="text" v-model="user.name">
          <button v-on:click="editUser(user)">SAVE</button>
        </div>

        <div v-else>
          <button v-on:click="edit = user.id">EDIT</button> -->
          {{ user.name }}
          {{ user.address.street }}
        <!-- </div> -->
      </li>
    </ul>
  </div>


</template>

<script>

import axios from 'axios';

export default {
  data() {
    return {
      users: [],
    };
  },
  created() {
    axios
      .get('http://jsonplaceholder.typicode.com/users')
      .then((response) => {
        this.users = response.data;
      })
      .catch((e) => {
        /* eslint-disable no-alert, no-console */
        console.log(e);
      });
  },
};
</script>
