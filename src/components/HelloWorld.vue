<template>
  <div>
    <router-link to="newcontact"><h1>{{ addSome }}</h1></router-link>
    <router-link to="todolist"><h1>{{ todoList }}</h1></router-link>
    <router-view></router-view>
  </div>
  
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      addSome: 'NEW',
      todoList: 'TODOLIST'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-weight: normal;
}

a {
  color: #42b983;
}
</style>
