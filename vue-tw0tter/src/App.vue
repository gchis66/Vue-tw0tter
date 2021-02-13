<template>
<div id="app">
  <nav>
    <router-link to="/">
    <div class="logo">
      Tw0tter
    </div>
    </router-link>
    <div class='nav-user' v-if="user">
      {{user.username}}
    </div>
  </nav>
<router-view/>
</div>

</template>

<script>
import { useStore } from 'vuex';
import { computed } from 'vue';

export default {
  name: 'App',
  setup() {
    const store = useStore();
    const user = computed(() => store.state.User.user);

    return{
      user
    }
  }
}
</script>

<style>
body{
  margin:0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #F3F5FA;
}
nav{
  width: 100%;
  height:50px;
  background-color:rgb(18, 137, 221);
  display:flex;
  align-items:center;
  justify-content: space-between;
}
.logo{
  font-size: 30px;
  color: white;
  font-weight: bold;
  padding-left: 40px;
}
a {
    text-decoration: none;
}
.nav-user{
  font-size: 30px;
  color: white;
  font-weight: bold;
  padding-right: 40px;
}
</style>
