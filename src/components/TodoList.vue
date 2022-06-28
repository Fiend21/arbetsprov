<template>
    <v-data-table :headers="headers" :items="todos" :item-key="id" :items-per-page="15" class="-1" :search="search">
        <template v-slot:top>
            <v-toolbar flat>
            <v-text-field id="search" v-model="search" placeholder="Find TODOS..."></v-text-field>
            <v-btn>Apply</v-btn>
            </v-toolbar>
        </template>

        <template v-slot:item.completed="{ item }">
            <v-simple-checkbox v-model="item.completed" disabled></v-simple-checkbox>
        </template>
        <template v-slot:item.actions="{ item }">
            <v-icon small class="mr-2" @click="editItem(item)">mdi-pencil</v-icon>
            <v-icon small @click="deleteItem(item)">mdi-delete</v-icon>
        </template>
    </v-data-table>
</template>

<script>
let id = 0

export default {
    name: 'TodoList',

    data() {
        return {
            headers: [
                {
                    text: 'Description',
                    sortable: true,
                    value: 'description',
                    align: 'Start',
                },

                {
                    text: 'Deadline',
                    value: 'deadline',
                },


                {
                    text: 'Created',
                    sortable: true,
                    value: 'created',
                },



                {
                    text: 'Completed',
                    sortable: false,
                    value: 'completed',
                },

                {
                    sortable: false,
                    value: 'actions',
                }
            ],
            todos: [
                { id: id++, created: '2022-06-23', description: 'Learn Vue.', deadline: '2022-06-29', completed: false },
                { id: id++, created: '2022-06-27', description: 'Learn Vuetify.', deadline: '2022-06-29', completed: false },
                { id: id++, created: '2022-06-27', description: 'Refactor .Net-app to use dedicated validation-class.', deadline: '2022-08-07', completed: false },
                { id: id++, created: '2022-06-28', description: 'Learn Play-framework.', deadline: '2022-06-29', completed: false }
            ]
        }
    }
}
</script>

<style>
#search {
    padding-left: 2.1em;
}
</style>