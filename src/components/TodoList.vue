<template>
    <v-data-table 
        :headers="headers" 
        :items="todos" 
        :item-key="id" 
        :items-per-page="15"        
        :search="search"
    >
        <template v-slot:top>
            <v-toolbar flat>
                <v-text-field 
                    id="search" 
                    v-model="search" 
                    placeholder="Find TODOS..."
                    append-icon="mdi-magnify"
                ></v-text-field>
                <v-spacer></v-spacer>
                <v-dialog 
                    v-model="dialog"
                    max-width="500px">
                    <template v-slot:activator="{ on, attrs }">
                        <v-btn
                            color="Black"
                            dark
                            class="mb-2"
                            v-bind="attrs"
                            v-on="on"
                        >New Todo</v-btn>
                    </template>
                     <v-card>
                        <v-card-title>
                            <span class="text-h5">{{ formTitle }}</span>
                        </v-card-title>
                     </v-card>
                </v-dialog>              
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
            <v-icon small class="mr-2" @click="editItem(item)">mdi-file-edit</v-icon>
            <v-icon small @click="deleteItem(item)">mdi-delete</v-icon>
        </template>
    </v-data-table>
</template>

<script>

export default {
    name: 'TodoList',

    data: () => ({

            dialog: false,
            dialogDelete: false,

            headers: [
                { text: 'Description',
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
            todos: [],
            editedIndex: -1,

            editedTodo: {
                    created: '', 
                    description: '', 
                    deadline: '', 
                    priority: '', 
                    completed: false 
            },

            defaultTodo: {
                    created: '', 
                    description: '', 
                    deadline: '', 
                    priority: '', 
                    completed: false 
            },
        }),

    computed: {
      formTitle () {
        return this.id === -1 ? 'New Todo' : 'Edit Todo'
      },
    },

     watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },

        created() {
            this.initialize()
        },

         methods: {
            initialize() {
                this.todos = [ {  
                    created: '2022-06-23',
                    description: 'Learn Vue.', 
                    deadline: '2022-06-29',
                    priority: 'High', 
                    completed: 
                    false 
                },

                {    
                    created: '2022-06-27', 
                    description: 'Learn Vuetify.', 
                    deadline: '2022-06-29', 
                    priority: 'High', 
                    completed: false 
                },

                {  
                    created: '2022-06-27', 
                    description: 'Refactor .Net-app to use dedicated validation-class.', 
                    deadline: '2022-08-07', 
                    priority: 'Low', 
                    completed: false 
                },

                {  
                    created: '2022-06-28', 
                    description: 'Learn Play-framework.', 
                    deadline: '2022-06-29', 
                    priority: 'Mid', 
                    completed: false 
                }]
            },

            editTodo (todo) {
                this.editedIndex = this.todos.indexOf(todo)
                this.editedTodo= Object.assign({}, todo)
                this.dialog = true
            },

            deleteItem (todo) {
                this.editedIndex = this.desserts.indexOf(todo)
                this.editedItem = Object.assign({}, todo)
                this.dialogDelete = true
            },

            deleteItemConfirm () {
                this.todos.splice(this.editedIndex, 1)
                this.closeDelete()
            },

            close () {
                this.dialog = false
                this.$nextTick(() => {
                this.editedTodo = Object.assign({}, this.defaultTodo)
                this.editedIndex = -1})
                },

            save () {
                if (this.editedIndex > -1) {
                    Object.assign(this.desserts[this.editedIndex], this.editedItem)
                    } else {
                    this.desserts.push(this.editedItem)
                    }
                    this.close()
                },    
        }
}
</script>

<style>
#search {
    padding-left: 0.3em;
}
</style>