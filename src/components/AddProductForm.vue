<template>
    <div>
       <form>
           <h4 class="text-center">Add product</h4>
            <div class="mb-3">
                <label class="form-label">Type ID</label>
                <select class="form-control" v-model="product.product_type_id">
                    <option disabled selected hidden>Change Type ID</option>
                    <option v-for="(productID, i) in productsID" :key="i" :value="productID.id" >{{ productID.name_uz }}</option>
                </select>
            </div>
            <div class="mb-3">
                <label class="form-label">Name</label>
                <input
                    v-model="product.name_uz"
                    type="text"
                    class="form-control"
                    placeholder="Name"
                    required
                >
            </div>
            <div class="mb-3">
                <label class="form-label">Cost</label>
                <input
                    v-model="product.cost"
                    type="number"
                    class="form-control"
                    required
                >
            </div>
            <div class="mb-3">
                <label class="form-label">Address</label>
                <input
                    v-model="product.address"
                    type="text"
                    class="form-control"
                    placeholder="Address"
                    required
                >
            </div>
            <div class="d-flex">
                <button @click="createProduct" class="btn btn-primary ml-auto">Add</button>
            </div>
        </form>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    props: {
        productsID: {
            type: Object,
        },
    },
    data () {
        return {
            product: {
                product_type_id: 0,
                name_uz: "",
                cost: 0,
                address: "",
                created_date: new Date().toISOString(),
            }
        }
    },
    methods: {
        // createProduct: function
        async createProduct() {
            axios.post('http://94.158.54.194:9092/api/product', this.product, {
                headers: {
                    'Content-Type': 'application/json',
                }
            })
            .then(response => this.$emit('addProduct', response.data))
            .catch(error => console.log(error))
        },
    },
}
</script>

