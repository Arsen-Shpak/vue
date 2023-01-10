<template>
     <form class="form">
        <h2> New post</h2>
        <my-input 
            v-model="post.title"
            type="text" 
            placeholder="name"
        />
        <my-input 
            v-model="post.body"
            type="text" 
            placeholder="body"
        />
        <my-buttons 
            @click="addPost"
            style="width: 50%;align-self: flex-end;margin-top: 15px;"
        >
            Add post
        </my-buttons>
    </form>
</template>

<script>

import myButtons from '@/components/UI/myButtons';
import myInput from '@/components/UI/myInput';

export default {

    components: { myButtons, myInput },
    
    data() {
        return {
            post: {
                title: "",
                body:"",
            }
        }
    },

    methods: {
        addPost(event) {
            event.preventDefault();
            this.post.id = Date.now(),

            this.$emit("addPost", this.post);

            this.post = {
                body : "",
                title : ""
            };
            
        }
    }
}
</script>


<style>
.form {
        display: flex;
        flex-direction: column;
    }

/* .input {
    width: 100%;
    border: 1px green solid;
    padding: 10px 15px;
    margin-top: 10px;
} */

/* .btn {
        align-self: flex-start;
        margin-top: 15px;
        padding: 10px 15px;
        background: none;
        color: green;
        border: 1px green solid;

    } */
</style>