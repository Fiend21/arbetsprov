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
                    single-line
                    hide-details
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
                         <v-card-text>
                             <v-container>
                                <v-row>
                                    <v-col>
                                        <v-text-field
                                            v-model="editedItem.description"
                                            label="Description"
                                        ></v-text-field>
                                    </v-col>
                                     <v-col>
                                        <v-text-field
                                            v-model="editedItem.deadline"
                                            label="YYYY-MM-DD"
                                        ></v-text-field>
                                    </v-col>
                                     <v-col>
                                        <v-text-field
                                            v-model="editedItem.priority"
                                            label="Priority"
                                        ></v-text-field>
                                    </v-col>
                                </v-row>
                             </v-container>
                        </v-card-text>

                        <v-card-actions>
                            <v-spacer></v-spacer>
                                <v-btn
                                    color="Black"
                                    text
                                    @click="close"
                                    >Cancel
                                </v-btn>
                                <v-btn
                                    color="Black"
                                    text
                                    @click="save"
                                    >Save
                                </v-btn>
                         </v-card-actions>
                     </v-card>
                </v-dialog>  
                <v-dialog v-model="dialogDelete" max-width="37em">
                    <v-card>
                        <v-card-title class="text-h5">
                            <p>Are you sure you want to delete this Todo?</p>
                        </v-card-title>
                        <v-card-actions>
                        <v-spacer></v-spacer>
                            <v-btn 
                                color="Black" 
                                text @click="closeDelete"
                                >Cancel
                                </v-btn>
                             <v-btn 
                                color="Black" 
                                text @click="deleteItemConfirm"
                                >OK
                                </v-btn>
                        <v-spacer></v-spacer>
                        </v-card-actions>
                     </v-card>
                 </v-dialog>            
            </v-toolbar>
        </template>

        <template v-slot:item.completed="{ item }">
            <v-simple-checkbox v-model="item.completed"></v-simple-checkbox> 
        </template>
        <template v-slot:item.actions="{ item }">
            <v-icon class="mr-2"
                @click="editItem(item)"
                >
                    mdi-file-edit
                </v-icon>
                <v-icon 
                    @click="deleteItem(item)"
                    >
                    mdi-delete
                </v-icon>
        </template>
    </v-data-table>
</template>

<script>

export default {
    name: 'TodoList',

    data: () => ({
            search: '',
            dialog: false,
            dialogDelete: false,

            headers: [],
            todos: [],
            editedIndex: -1,

            editedItem: {
                    created: '', 
                    description: '', 
                    deadline: '', 
                    priority: '', 
                    completed: false 
            },

            defaultItem: {
                    created: '', 
                    description: '', 
                    deadline: '', 
                    priority: '', 
                    completed: false 
            },
        }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New Todo' : 'Edit Todo'
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
                this.headers =  [{   
                    text: 'Description',
                    sortable: true,
                    value: 'description',
                    align: 'Start',
                },

                {
                    text: 'Priority',
                    sortable: false,
                    value: 'priority',
                },

                {
                    text: 'Deadline',
                    sortable: false,
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

                this.todos = [ {  
                    created: '2022-06-23',
                    description: 'Learn Vue.', 
                    deadline: '2022-06-29',
                    priority: 'High', 
                    completed: false 
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
                }
            ]
            },



            editItem (item) {
                this.editedIndex = this.todos.indexOf(item)
                this.editedItem = Object.assign({}, item)
                this.dialog = true
            },

            deleteItem (item) {
                this.editedIndex = this.todos.indexOf(item)
                this.editedItem = Object.assign({}, item)
                this.dialogDelete = true
            },

            deleteItemConfirm () {
                this.todos.splice(this.editedIndex, 1)
                this.closeDelete()
            },

            close () {
                this.dialog = false
                this.$nextTick(() => {
                this.editedItem = Object.assign({}, this.defaultItem)
                this.editedIndex = -1})
                },

            closeDelete () {
                this.dialogDelete = false
                this.$nextTick(() => {
                this.editedItem = Object.assign({}, this.defaultItem)
                this.editedIndex = -1
            })
      },    

            save () {
                if (this.editedIndex > -1) {
                    Object.assign(this.todos[this.editedIndex], this.editedItem)
                    } else {
                    this.todos.push(this.editedItem)
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

.h5 {
    justify-content: center;
}
</style>