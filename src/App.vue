<template>
  <v-app id="Arbetsprov">
    <v-navigation-drawer
      v-model="drawer"
      app
    ></v-navigation-drawer>

  <v-app-bar app>
     <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
     <v-toolbar-title>TodoList</v-toolbar-title>
  </v-app-bar>

    <v-main>
      <TodoList/>
    </v-main>
  </v-app>
</template>

<script>
import TodoList from './components/TodoList';

export default {
  name: 'App',

  components: {
    TodoList,
},

  data: () => ({
    drawer: null
  }),
};
</script>
