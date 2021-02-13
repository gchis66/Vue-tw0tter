<template>
  <div class="home">
<h1>Home</h1>

<div class="users-list">
  <router-link v-for="user in users" :to="{ name: 'UserProfile', params: {userId: user.id} }" :key="user.id">
    {{user.username}}
  </router-link>
</div>
  </div>
</template>

<script>
import {users} from "../assets/users"

export default {
  name: 'Home',
  setup(){
    return {
      users
    }
  }

}
</script>

<style scoped>
h1 {
  padding-left: 40px;
}

.users-list{
  display:flex;
  flex-direction: column;
  font-size: 20px;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: bold;
}
</style>