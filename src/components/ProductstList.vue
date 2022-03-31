<template>
    <tbody>
        <tr v-for="product in products" v-bind:key="product.id">
          <th scope="row">{{product.id}}</th>
          <td><p>{{product.product_type_id}}</p></td>
          <td><p>{{product.name_uz}}</p></td>
          <td><p>{{product.address}}</p></td>
          <td><p>{{product.cost}}</p></td>
          <td>
            <button @click="$emit('edit', product)" class="btn btn-secondary"><span class="material-icons d-block">edit</span></button>
            <button @click="$emit('remove', product)" class="btn btn-danger mx-1"><span class="material-icons d-block">delete</span></button>
            </td>
        </tr>
    </tbody>
</template>

<script>
export default {
    props: {
        products: {
            type: Array,
            required: true
        },
    },
}
</script>
