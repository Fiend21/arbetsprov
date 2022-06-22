<template>
    <v-data-table
        :headers="headers"
        :items="todos"
        :item-key="id"
        class="-1"
    ></v-data-table>
</template>

<script>
    let id = 0
    export default {
        name: 'TodoList',

        data() {
            return {
                headers: [
                    {text: 'TODO',
                     value: 'title',
                    }
                ],
                todos: [
                    {id: id++, title: 'Learn Vue'},
                    {id: id++, title: 'Learn Vuetify'},
                ]
            }
        }
    }
</script>