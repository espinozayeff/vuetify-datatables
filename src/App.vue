<template>
    <v-app>
        <v-content>
            <v-container class="mt-10">
                <H1>hola</H1>
                <DataTable>
                    <template scope="header">
                        Cabecera X
                    </template>
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

                <!--<DataTable>
                    <template v-slot:item.address="{ item }">
                        <p>
                            Direccion de prueba.
                            <small>{{ item.address }}</small>
                        </p>
                    </template>
                </DataTable>-->
                <!--<TestParent>
                    <template v-slot:column.x>
                        <h6>Columna x</h6>
                    </template>
                </TestParent>-->
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
