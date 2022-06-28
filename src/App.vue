<template>
  <v-app id="Arbetsprov">
    <v-app-bar app>
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
  }),
};
</script>
