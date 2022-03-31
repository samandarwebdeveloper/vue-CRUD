<template>
    <thead>
        <tr>
            <th scope="col">#</th>
            <th scope="col">Type ID</th>
            <th scope="col">Name</th>
            <th scope="col">Address</th>
            <th scope="col">Count</th>
            <th scope="col"><button @click="showModal" class="btn btn-primary"><span class="material-icons d-block">add</span></button></th>
        </tr>
    </thead>
</template>

<script>
export default {
    props: {
        showModal: {
            type: Function,
        }
    },
}
</script>

<style>

</style>