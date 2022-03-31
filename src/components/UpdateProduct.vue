<template>
    <div>
        <h4 class="text-center">Edit {{ product.id }}</h4>
        <form @submit="updateProduct">
            <div class="mb-3">
                <label class="form-label">Type ID</label>
                <select class="form-control" v-model="product.product_type_id">
                    <option disabled selected hidden>{{product.product_type_id}}</option>
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
                    required
                >
            </div>
        </form>
            <div class="d-flex">
                <button @click="updateProduct" class="btn btn-primary ml-auto">Update</button>
            </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    props: {
        productsID: {
            type: Object,
        },
        product: {
            type: Object,
        },
    },
    methods: {
        // updateProduct: function 
        async updateProduct() {
            axios.put('http://94.158.54.194:9092/api/product', this.product, {
                headers: {
                    'Content-Type': 'application/json',
                }})
            .then(response => {
                this.$emit('hideUpModal', response.data)
            })
            .catch(error => console.log(error))
        },
    },

}
</script>
