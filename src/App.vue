<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>

  <h1>Bucketlist</h1>

  <form @submit.prevent="voegLifeGoal">
    <label>Voeg een nieuw life-goal toe</label>
      <input v-model="lifeGoal" name="lifeGoal">
      <button>Toevoegen</button>
  </form>
  <ul>
    <li v-for="goal in goals" :key="todo.id">
      <h3 @click="toggleDone(goal)">{{goal.content}}</h3>
    </li>
  </ul>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import { ref } from 'vue';

export default {
  name: 'App',
  components: {
    HelloWorld
  }

  setup(){

    const lifeGoal = ref('');
    const goals = ref([]);

    function voegLifeGoal(){
      goals.value.push({
        id: new Date.now(),
        done: false,
        content: lifeGoal.value,
      });
      lifeGoal.value = '';
    }

    function toggleDone(goal){
      goal.done = !goal.done;
    }

    return {
      goals,
      lifeGoal,
      voegLifeGoal,
      toggleDone,
    };

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.done{
  text-decoration:line-through;
}
</style>
