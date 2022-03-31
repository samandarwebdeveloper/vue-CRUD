<template>
    <div class="modal" v-if="show" @click.stop="hideModal">
        <div @click.stop class="modal-content">
            <slot @hideModal="hideModal"></slot>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        show: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        hideModal() {
            this.$emit('update:show', false)
        },
    }
}
</script>

<style>
.modal {
    position: fixed;
    display: flex;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    z-index: 9999;
}
.modal-content {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: #fff;
    width: 500px;
    padding: 20px;
    border-radius: 5px;
}
</style>