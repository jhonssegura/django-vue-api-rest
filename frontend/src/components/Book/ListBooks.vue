<template lang="html">
    <div class="container">
        <div class="row">
            <div class="col text-left">
                <h2>Listado de Libros</h2>

                <div class="col-md-12">
                    <b-table striped hover :items="books" :fields="fields">
                        <template v-slot:cell(action)="data"> 
                            <b-button size="sm" variant="primary">
                                Editar
                            </b-button>
                            <b-button size="sm" variant="danger">
                                Eliminar
                            </b-button>
                        </template>
                    </b-table>
                </div>
            </div>
        </div>
    </div>

</template>

<script>
import axios from 'axios';

export default {
    data () {
        return {
            fields: [
                {key: 'title', label: 'Título'},
                {key: 'description', label: 'Descripción'},
                {key: 'action', label: 'Acción'}
            ],
            books: []
        }
    },
    methods: {
        getBooks () {
            const path = 'http://localhost:8000/api/v1/books/'
            axios.get(path).then((response) => {
                this.books = response.data
            })
            .catch((error) => {
                console.log(error)
            })
        }
    },
    created() {
        this.getBooks()
    }
}
</script>

<style lang="css" scoped>

</style>