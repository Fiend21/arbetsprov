<template>
  <v-app id="inspire">
    <v-app-bar app>
      <v-toolbar-title>TodoList v.1.0</v-toolbar-title>
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
  }),
};
</script>
