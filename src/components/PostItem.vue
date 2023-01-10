<template>
    <div class="post">
        <div>
            <div>Name: <strong> {{ post.title }}</strong></div>
            <div> Describe:{{ post.body }}</div>
        </div>
        <div>
            <my-buttons 
                @click="this.$emit('remove',post)"
            >
                Delete
            </my-buttons>
        </div>
       
    </div>
</template>   

<script>
import myButtons from '@/components/UI/myButtons';

export default {
    components: {
            myButtons
    },
        
        props: {
            post: {
                type: Object,
                required:true,
            }
        }

        // methods: {
        //     deletePost() {
        //          this.$emit("deletePost", post);
        //     }
        // }
    }
</script>

<style>

.post {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 15px;
        border: 2px green solid;
        margin-top: 15px;
    }

 .list {
    margin-top: 10px;
 }
</style>