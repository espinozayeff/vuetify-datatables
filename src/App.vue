<template>
    <v-app>
        <v-content>
            <v-container class="mt-10">
                <H1>hola</H1>
                <DataTable>
                    <h1 slot="header">Custom Header Table</h1>
                    <template v-slot:item.address="{ item }">
                        <p>
                            <strong>Prueba Address</strong>: {{ item.address }}
                        </p>
                    </template>
                    <template v-slot:item.isActive="{ item }">
                        <el-tag
                            size="medium"
                            :color="item.isActive ? 'green' : 'orange'"
                        >
                            item.isActive
                        </el-tag>
                    </template>
                </DataTable>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>
import DataTable from './components/data-table'
export default {
    name: 'App',
    components: {
        // TestParent: () => import('./components/test-parent'),
        DataTable,
        // Wrapper: () => import('./components/Wrapper'),
    },
    data() {
        return {
            DataTable,
        }
    },
}
</script>
