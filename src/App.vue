<template>
    <v-app>
        <v-content>
            <v-container class="mt-10">
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
                    <template v-slot:top>
                        <el-switch
                            v-model="singleSelect"
                            active-text="Activo"
                            class="m-3"
                        >
                        </el-switch>
                    </template>
                    <template v-slot:item.isActive="{ item }">
                        <el-tag size="medium" :color="getColor(item.isActive)">
                            item.isActive
                        </el-tag>
                    </template>
                    <template v-slot:item.address="{ item }">
                        <el-tooltip placement="left">
                            <div slot="content">
                                {{ item.address }}
                            </div>
                            <p class="cr-pointer">
                                Dirección
                            </p>
                        </el-tooltip>
                    </template>
                    <template v-slot:item.actions="{ item }">
                        <el-popover
                            placement="bottom-left"
                            width="150"
                            trigger="click"
                        >
                            <div
                                class="row mx-0 p-1 hover-options"
                                @click="updateItem(item)"
                            >
                                Editar
                            </div>
                            <div
                                class="row mx-0 p-1 hover-options"
                                @click="deleteItem(item)"
                            >
                                Eliminar
                            </div>
                            <i
                                slot="reference"
                                class="mdi mdi-dots-vertical f-23 cr-pointer"
                            />
                        </el-popover>
                    </template>
                </v-data-table>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>
import axios from 'axios'
export default {
    name: 'App',

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

    mounted() {
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
                const { data } = await axios('http://localhost:4000/clients')
                this.clients = data
            } catch (error) {
                console.error(error)
            }
        },
    },
}
</script>
