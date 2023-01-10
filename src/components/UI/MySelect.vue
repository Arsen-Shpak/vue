<template>
    <select v-bind:value="modelValue" @change="changeOption">
        <option 
            value="" 
            disabled
        > 
            Choose selecet
        </option>
        <option 
            v-for="option in options"
            :value="option.value" 
            :key="option.value"
        > 
           {{ option.name }}
        </option>

    </select>
</template>

<script>
    export default {
        name: 'my-select',

        props: {
            modelValue: {
                type:String
            },

            options: {
                type: Array,
                default:()=>[]
            }
        },

        methods: {
            changeOption(event) {
                this.$emit('update:modelValue', event.target.value)
            }
        }
    }
</script>

<style></style>

