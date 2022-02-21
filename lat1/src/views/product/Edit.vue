<template>
    <div class="container my-5">
        <div class="col-8">
            <router-link :to="{ name: 'product.index'}"
            class="btn btn-primary btn-sm rounded shadow mb-3"
            >Back</router-link>
            <div class="card rouded shadow">
                <div class="card-header">
                    Create New Product
                </div>
                <div class="card-body">
                    <form @submit.prevent="update()">
                        <div class="mb-3">
                            <label for="" class="form-label">Name</label>
                            <input type="text" class="form-control" v-model="product.name">
                            <div v-if="validation.name" class="text-danger">
                                {{ validation.name[0] }}
                            </div>
                        </div>
                        <div class="mb-3">
                            <label for="" class="form-label">Price</label>
                            <input type="number" class="form-control" v-model="product.price">
                            <div v-if="validation.price" class="text-danger">
                                {{ validation.price[0] }}
                            </div>
                        </div>
                        <div class="mb-3">
                            <label for="" class="form-label">Description</label>
                            <textarea name="" id="" cols="30" rows="10" class="form-control" v-model="product.description"></textarea>
                            <div v-if="validation.description" class="text-danger">
                                {{ validation.description[0] }}
                            </div>
                        </div>
                        <div class="mb-3">
                            <label for="" class="form-label">Category</label>
                            <input type="text" class="form-control" v-model="product.category_id">
                            <div v-if="validation.category_id" class="text-danger">
                                {{ validation.category_id[0] }}
                            </div>
                        </div>
                        <button class="btn btn-outline-primary">Submit</button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import { reactive, ref, onMounted } from "vue"
import { useRouter, useRoute } from "vue-router"
import axios from "axios"
export default {
    setup() {
        //data binding
        let product = reactive({
            name: '',
            description: '',
            price: '',
            category_id: ''
        });
        const validation = ref([]);

        const router = useRouter();
        const route = useRoute();
        onMounted(() => {
            axios.get(`http://api.cartel.loc/api/products/${route.params.id}`)
            .then((result) => {
                product.name = result.data.data.name
                product.price = result.data.data.actual_price
                product.description = result.data.data.description
                product.category_id = result.data.data.category.id
                console.log(result.data)
            }).catch((err) => {
                console.log(err.response.data)
            });
        });

        function update() {
            axios({
                method: 'put',
                url: `http://api.cartel.loc/api/products/${route.params.id}`,
                data: product,
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json',
                    'Authorization': 'Bearer 1|7qn88rozvkHEZrItgVKaKebVEzr5lLpkHblFBRE7'
                }
            })
            .then(function () { 
                router.push({
                    name: 'product.index'
                });
            }).catch((err) => {
                validation.value = err.response.data.errors
                //console.log(err.response.data.errors.category_id);
            });            

        }
        return {
            product,
            validation,
            router,
            route,
            update
        }

    }
}
</script>