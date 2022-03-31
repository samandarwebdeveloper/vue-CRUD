<template>
  <div class="px-4">
    <table class="table table-striped table-hover">
        <products-head :showModal="showModal" /> <!-- this is the component --> 
        <productst-list 
          :products="products" 
          @edit="editProduct" 
          @remove="removeProduct"
        /> <!-- this is the component -->
    </table>
    <my-modal v-model:show="modalWisible">
      <add-product-form 
        :productsID="productsID"
      /> <!-- this is the component -->
    </my-modal>
    <update-modal v-model:show="modalUpWisible" >
      <update-product @hideUpModal="modalUpWisible=!modalUpWisible"  
        :product="product"
        :productsID="productsID"
      /> <!-- this is the component -->
    </update-modal>
    <div class="d-flex">
      <p class="mx-auto" v-show="products.length===0" ><b class="h2 text-danger">Empty</b></p>
    </div>
    <div class="fixed-bottom d-flex pr-5">
      <p class="ml-5">This: <b>{{page}}</b> page</p>
      <nav class="mx-auto" aria-label="Page navigation example">
        <ul class="pagination">
          <li class="page-item"><button class="page-link" @click="changePagePrev" href="#">Previous</button></li>
          <li class="page-item"><button class="page-link" @click="changePageNext" href="#">Next</button></li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
import axios from 'axios' // axios is a library for making http requests
import ProductsHead from './components/ProductsHead' // this is the component
import ProductstList from './components/ProductstList' // this is the component
import AddProductForm from './components/AddProductForm' // this is the component
import MyModal from './components/UI/MyModal'   // this is the component
import UpdateProduct from './components/UpdateProduct' // this is the component
import UpdateModal from './components/UI/UpdateModal' // this is the component

export default {
  components: {
    ProductsHead,
    ProductstList,
    MyModal,
    AddProductForm,
    UpdateProduct,
    UpdateModal,
  },
  // data is a function that returns an object
  data() {
    return {
      products: [],
      product: [],
      productsID: [],
      modalWisible: false,
      modalUpWisible: false,
      page: 1,
      perPage: 5,
      totalRows: 0,
    }
  },
  // computed properties are functions that return values
  methods: {
    showModal() {
      this.modalWisible = true
    },
    hideUpModal() {
      this.modalWisible = false
    },
    changePagePrev() {
      if (this.page > 1) {
        this.page--
        this.fetchData()
      }
    },
    changePageNext() {
      if(this.products.length >= this.perPage){
        this.page++
        this.fetchData() 
      }
    },
    // this is the method that fetches the data from the server
    async fetchData() {
      try {
        const response = await axios.get('http://94.158.54.194:9092/api/product', {
          params: {
            page: this.page,
            perPage: this.perPage
          }
        });
        // this.totalRows = Math.ceil(response.headers['x-total-count'] / this.perPage) // this is the total number of rows
        this.products = response.data;
      } catch  {
        alert('Server error')
      }
    },
    async fetchId() {
      try {
        const response = await axios.get('http://94.158.54.194:9092/api/product/get-product-types')
        this.productsID = response.data
      } catch {
        console.log('FetchId server not working')
      }
    },
    // this is the method that edited a product
    editProduct(product) {
      this.id = product.id
      this.product_type_id = product.product_type_id
      this.name_uz = product.name_uz
      this.cost = product.cost
      this.address = product.address
      this.product = product
      this.modalUpWisible = true
    },
    // this is the method that removes a product
    removeProduct(product) {
      axios.delete('http://94.158.54.194:9092/api/product/' + product.id)
      .then(response => {
        this.products = this.products.filter(p => p.id !== product.id)
      })
    }
  },
  // this is the method that runs when the component is created
  mounted() {
    this.fetchData();
    this.fetchId();
  }
}
</script>