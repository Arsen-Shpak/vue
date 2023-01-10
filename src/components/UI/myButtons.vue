<template>
    <button class="btn">
        <slot></slot>
        <!-- <slot></slot> -->
    </button>
</template>

<script>
export default {
        name:'my-buttons'
    }
</script>

<style scoped>

.btn {
        
        padding: 10px 15px;
        background: none;
        color: green;
        border: 1px green solid;

    }
</style>