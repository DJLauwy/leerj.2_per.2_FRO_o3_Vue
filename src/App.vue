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
  <button @click="removeAllGoals">Alle goals verwijderen ('New year, new me' gevalletje?)</button>
  <button @click="markAllDone">Alles afstrepen (Je hebt blijkbaar geen doelen meer in je leven)</button>
  <ul>
    <li v-for="(goal, index) in goals" :key="todo.id" class="goal">
      <h3 :class="{ done: goal.done }" @click="toggleDone(goal)">{{goal.content}}</h3>
      <button @click="removeGoal(index)">X</button>
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

    function removeGoal(index){
      goals.value.splice(index, 1);
    }

    function markAllDone(){
      goals.value.forEach((goal) => goal.done = true);
    }

    function removeAllGoals(){
      goals.value = [];
    }

    return {
      goals,
      lifeGoal,
      voegLifeGoal,
      toggleDone,
      removeGoal,
      markAllDone,
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

.goal{
  cursor: pointer;
}

.done{
  text-decoration:line-through;
}
</style>
