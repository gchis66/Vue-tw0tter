<template>
<div class="user-profile">
    <div class="user-profile_user-panel">
  <h1 class="user-profile_username">@{{ state.user.username}}</h1>
  <div class="admin-badge" v-if="state.user.isAdmin">Admin</div>
<div class="user-profile_follower-count"><strong>Followers:</strong> {{state.followers}}</div>
  
  <button id="followBtn" @click="followUser">
    Follow
  </button>

  <form class="user-profile_create-tw33t" @submit.prevent="createNewTw33t" :class="{ 'exceeded': newTw33tCharacterCount > 180 }">
      <label for="newTw33t"><strong>New Tw33t</strong>({{newTw33tCharacterCount}}/180)</label>
      <textarea id="newTw33t" rows="4" v-model="state.newTw33tContent"/>

      <div class="user-profile_create-tw33t-type">
          <label for="newTw33tType"><strong>Type:</strong></label>
          <select id="newTw33tType" v-model="state.selectedTw33tType">
              <option :value="option.value" v-for="(option, index) in state.tw33tTypes" :key="index">
                  {{option.name}}
              </option>
          </select>
      </div>

      <button id="tw33tButton">
          Tw33t!
      </button>

  </form>
</div>
  <div class = "user-profile_tw33ts-wrapper">
        <Tw33tItem
            v-for="tw33t in state.user.tw33ts" 
            :key="tw33t.id" 
            :username="state.user.username" 
            :tw33t="tw33t" 
        />
  </div>
  </div>

</template>

<script>
import { reactive, computed } from 'vue';
import Tw33tItem from "../components/Tw33tItem.vue";
import { useRoute } from 'vue-router';
import { users } from "../assets/users";

export default {
  name: 'UserProfile',
  components: { Tw33tItem },
  setup(){
    const route = useRoute();
    const userId = computed(() => route.params.userId)

    const state = reactive({
      followers: 0,
      user:users[userId.value - 1] || users[0],
      newTw33tContent: '',
      selectedTw33tType: 'instant',  
      tw33tTypes: [
          { value: 'draft', name:'Draft'},
          { value: 'instant', name:'Instant Tw33t'}
      ],

    })

  const newTw33tCharacterCount = computed(() => state.newTw33tContent.length)

    function followUser() {
      state.followers++
    }

    function createNewTw33t() {
        if(state.newTw33tContent && state.selectedTw33tType !== 'draft'){
            state.user.tw33ts.unshift({
                id:state.user.tw33ts.length + 1,
                content:state.newTw33tContent
            })
            state.newTw33tContent = '';
        }
    }

/*     function newTw33tCharacterCount() {
        return state.newTw33tContent.length;
    } */
    return {
      state,
      followUser,
      createNewTw33t,
      newTw33tCharacterCount,
      userId

    }
  }
};
</script>

<style scoped>
.user-profile_create-tw33t.exceeded {
    border-color: red;
    color: red;
}

.user-profile_create-tw33t.exceeded > button {
    background-color: red;
    border: none;
    color: white;
}

        .admin-badge{
        background:rgb(18, 137, 221);
        color:white;
        border-radius: 5px;
        margin-right:auto;
        padding: 0 10px;
        font-weight:bold;
        margin-top:5px;
        }
        h1 {
        margin: 0;
        }

                .user-profile_create-tw33t{
        display:flex;
        flex-direction: column;
        padding-top: 20px;
        }
.user-profile_create-tw33t-type{
    margin-top: 10px;

}
#tw33tButton{
    margin-top: 10px;
}

#followBtn{
    width:150px;
    margin-bottom: 5px;
}


.user-profile{
  display:grid;
  grid-template-columns: 1fr 2fr 1fr;
  padding: 50px 5%;
}

  .user-profile_user-panel {
    display:flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    height: 300px;
    }


</style>