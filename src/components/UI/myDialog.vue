<template>
    <div class="dialog" v-if="show" @click="hideDialog">
        <div class="dialog__content" @click.stop>
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: 'my-dialog',

    props: {
        show: {
            type: Boolean,
            default:true,
        }
    },

    methods: {
        hideDialog() {
           this.$emit('update:show',false)
        }
    }
}
</script>

<style>

.dialog {
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    background: rgba(0,0,0,0.5);
    position: fixed;
    display: flex;
}

.dialog__content {
    margin: auto;
    padding: 20px;
    background: white;
    border-radius: 20px;
    min-width: 100px;
}
</style>