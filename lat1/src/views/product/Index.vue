<template>
    <div class="container my-5">
        <div class="col-12">
            <router-link :to="{ name: 'product.create'}"
            class="btn btn-primary btn-sm rounded shadow mb-3"
            >Add</router-link>
            <div class="card rounded shadow">
                <div class="card-header">
                    Product List
                </div>
                <div class="card-body">
                    <table class="table">
                        <thead>
                            <tr>
                                <th>Name</th>
                                <th>price</th>
                                <th>Description</th>
                                <th>Category</th>
                                <th>Action</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(product, index) in products.data" :key="index"> <!--INDEX ADALAH INDEX ELEMENT UNTUK MENGHAPUS ELEMENT-->
                                <td>{{ product.name }}</td>
                                <td>{{ product.price }}</td>
                                <td>{{ product.description }}</td>
                                <td>{{ product.category }}</td>
                                <td>
                                    <div class="btn-group">
                                        <router-link
                                        :to="{ name: 'product.edit', params:{id: product.slug}}"
                                        class="btn btn-sm btn-outline-info"
                                        >Edit
                                        </router-link>
                                        <!--INDEX ADALAH INDEX ELEMENT DARI VALUE DIATAS-->
                                        <button class="btn btn-sm btn-outline-danger" @click.prevent="destroy(product.slug, index)">Delete</button>                                        
                                    </div>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from "axios"
import { onMounted, ref } from "vue"
export default {
    setup() {
        let products = ref([]);
        onMounted(() => {
            axios.get('http://api.cartel.loc/api/products')
            .then((result) => {
                products.value = result.data
            }).catch((err) => {
                console.log(err.response)
            });
        });
        function destroy(id, index) {
            axios({
                method: 'delete',
                url: `http://api.cartel.loc/api/products/${id}`,
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json',
                    'Authorization': 'Bearer 1|7qn88rozvkHEZrItgVKaKebVEzr5lLpkHblFBRE7'
                }
            })
            .then(function () { 
                products.value.data.splice(index, 1)
            }).catch((err) => {
                console.log(err.response.data);
            });            

        }

        return { 
            products, 
            destroy
        }
    }
}
</script>