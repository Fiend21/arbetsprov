<template>
  <v-app id="Arbetsprov">
    <v-navigation-drawer
      v-model="drawer"
      app
    >
    <v-list-item>
      <v-list-item-content>
        <v-list-item-title>Display Options</v-list-item-title>
        <v-list-item-subtitle>- Select a Subset</v-list-item-subtitle>
      </v-list-item-content>  
    </v-list-item>
  <v-divider></v-divider>
     
    <v-list
      dense
      nav
    ></v-list>

         <v-list-item
          v-for="subset in subsets"
          :key="subset.title"
        >
          <v-list-item-icon>
            <v-icon>{{ subset.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ subset.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
    </v-navigation-drawer>

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
    drawer: null,

    subsets: [
      {title: 'Current', icon: 'mdi-timer-sand-empty', todos: [{}]},
      {title: 'Previous', icon: 'mdi-check', todos: [{}]},
      {title: 'All', icon: 'mdi-all-inclusive', todos: [{}]},    
      ],
  }),
};
</script>
