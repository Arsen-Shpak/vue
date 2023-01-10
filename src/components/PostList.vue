
<template>
    <div v-if="posts.length > 0">
        <h3 class="list">List of posts</h3>
        <transition-group name="post-list">
            <post-item 
            :key="post.id"
            class="post" 
            v-for="post in posts"
            :post = "post"
            @remove="this.$emit('remove',post)"
        />
        </transition-group>
        
    </div>
    <h2 v-else style="color:red"> List is empty</h2>
    <!-- <div class="post" v-for="post in posts">
       <div>Name: <strong> {{ post.title }}</strong></div>
        <div> body:{{ post.body }}</div>
    </div> -->
</template>

<script>
import PostItem from './PostItem.vue';

export default {
    components: { PostItem },

    props: {
        posts: {
            type: Array,
            required:true,
        }
    }
}
</script>

<style scoped>
 /* .post {
        padding: 15px;
        border: 2px green solid;
        margin-top: 15px;
    } */

 .list {
    margin-top: 10px;
 }

 .post-list-item {
    display: inline-block;
    margin-right: 10px;
 }

 .post-list-enter-active,
 .post-list-leave-active{
    transition: all 1s ease;
 }
 .post-list-enter-from,
 .post-list-leave-to{
    opacity:0;
    transform:translateY(30px);
 }
 .post-list-move{
    transition: transform 1s ease;

 }
</style>