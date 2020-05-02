<template>
    <section>
        <slot name="header">Header</slot>
        <el-input v-model="search" />
        <v-data-table
            :headers="headers"
            :items="clients"
            :single-select="singleSelect"
            :search="search"
            :options="options"
            :show-select="showSelect"
            :footer-props="footerOptions"
            class="elevation-1"
            v-model="selected"
        >
            <!-- Vuetify Column definition -->
            <template
                v-for="name in columns"
                :slot="name"
                slot-scope="slotData"
            >
                <!-- Child Column template -->
                <slot :name="name" v-bind="slotData" />
            </template>
        </v-data-table>
        <slot name="footer">Footer</slot>
    </section>
</template>

<script>
import axios from 'axios'

export default {
    name: 'data-table',
    props: [],
    data() {
        return {
            options: {
                itemsPerPage: 10,
                itemKey: 'id',
                locale: 'es-ES',
            },
            footerOptions: {
                itemsPerPageOptions: [5, 25, 50, -1],
                itemsPerPageText: 'Registros por página',
            },
            showSelect: true,
            headers: [
                {
                    text: 'Código',
                    value: 'multileve.id',
                    filterable: false,
                },
                {
                    text: 'Estado',
                    value: 'isActive',
                    sortable: false,
                    filterable: false,
                },
                {
                    text: 'Edad',
                    value: 'age',
                },
                {
                    text: 'Nombre',
                    value: 'name',
                },
                {
                    text: 'Sexo',
                    value: 'gender',
                },
                {
                    text: 'Dirección',
                    value: 'address',
                },
                {
                    text: 'Fecha de registro',
                    value: 'registered',
                },
                {
                    text: 'Actions',
                    value: 'actions',
                    sortable: false,
                },
            ],
            clients: [],
            singleSelect: false,
            selected: [],
            search: null,
        }
    },
    computed: {
        columns() {
            return Object.keys(this.$scopedSlots).filter(c =>
                c.startsWith('item.'),
            )
        },
    },
    mounted() {
        console.log('Scoped', this.$scopedSlots)
        console.log('Slots', this.$slots)
        this.fetchData()
    },
    methods: {
        getColor(isActive) {
            return isActive ? 'green' : 'orange'
        },
        updateItem(item) {
            console.log('Updating item', item)
        },
        deleteItem(item) {
            console.log('Deleting item', item)
        },
        async fetchData() {
            try {
                const { data } = await axios('http://localhost:3000/clients')
                this.clients = data
            } catch (error) {
                console.error(error)
            }
        },
    },
}
</script>

<style scoped></style>
