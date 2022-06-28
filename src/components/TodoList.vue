<template>
    <v-data-table :headers="headers" :items="todos" :item-key="id" :items-per-page="15" class="-1" :search="search">
        <template v-slot:top>
            <v-toolbar flat>
                <v-text-field 
                    id="search" 
                    v-model="search" 
                    placeholder="Find TODOS..."
                    append-icon="mdi-magnify"
                ></v-text-field>
                <v-spacer></v-spacer>
                <v-switch
                    v-model="singleExpand"
                    label="Hide Completed"
                    class="mt-2"
                ></v-switch>
                <v-spacer></v-spacer>
                <template>
                    <v-btn
                        color="primary"
                        dark
                        class="mb-2"
                        v-bind="attrs"
                        v-on="on"
                    >New Todo</v-btn>
                </template>
            </v-toolbar>
        </template>

        <template v-slot:item.completed="{ item }">
            <v-simple-checkbox v-model="item.completed" disabled></v-simple-checkbox>
        </template>
        <template v-slot:expanded-item="{ headers, item }">
            <td :colspan="headers.length">
                Details about {{ item.name }}
            </td>
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

    data: () => ({
         
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
                    text: 'Priority',
                    value: 'priority',
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
                { id: id++, created: '2022-06-23', description: 'Learn Vue.', deadline: '2022-06-29', priority: 'High', completed: false },
                { id: id++, created: '2022-06-27', description: 'Learn Vuetify.', deadline: '2022-06-29', priority: 'High', completed: false },
                { id: id++, created: '2022-06-27', description: 'Refactor .Net-app to use dedicated validation-class.', deadline: '2022-08-07', priority: 'Low', completed: false },
                { id: id++, created: '2022-06-28', description: 'Learn Play-framework.', deadline: '2022-06-29', priority: 'Mid', completed: false }
            ]
        })
}
</script>

<style>
#search {
    padding-left: 0.3em;
}
</style>