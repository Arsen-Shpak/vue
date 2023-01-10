<template >
    <div > 
        <h2>Create new post</h2>
        <my-input 
            v-model="searchQuery"
            placeholder="Search"
        />
        <div class="app__btns">
            <my-buttons @click="openDialog">
                Create
            </my-buttons>
            <my-select 
                v-model="selectedSort"
                :options="sortOptions"
            />
        </div>
        <!-- <my-buttons @click="fetchPosts"> запрос</my-buttons> -->
        
        <my-dialog v-model:show="isOpenDialog">
            <post-form  @addPost = "addPost" />
        </my-dialog>
            <!-- <input type="text" v-model.number="str"> -->

        <post-list :posts="filterAndSort" @remove="removePost" v-if="!isPostsLoading"/>
        <div v-else> Loading...</div>
        <div class="page__wrapper">
            <div 
                v-for="pageNumber in totalPages" 
                :key="pageNumber"
                class="page"
                :class="{'current-page':pageNumber === page}"
                @click="changePage(pageNumber)"
            >
                {{ pageNumber }}
            </div>
        </div>
    </div>
</template>

<script>

import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';
import myDialog from '@/components/UI/myDialog.vue';
import myButtons from '@/components/UI/myButtons.vue';
import axios from 'axios';
import MySelect from '@/components/UI/MySelect.vue';
import myInput from '@/components/UI/myInput.vue';

export default {
    components: {
      PostForm, PostList, myDialog,myButtons,MySelect,myInput
    },

    data() {
        return {
            posts: [],
            // title: "",
            // body:"",
            isOpenDialog: false,
            isPostsLoading:false,
            // str:"",
            selectedSort: "",
            sortOptions: [
                { value: 'title', name: 'название' },
                {value:'body',name:'описанию'},
            ],
            searchQuery: "",
            page: 1,
            limit: 10,
            totalPages:0,
        }
    },
    methods: {
        addPost(post) {
            this.posts.push(post);
            this.isOpenDialog = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(item => item.id !== post.id);
        },
        openDialog() {
            this.isOpenDialog = true;
        },
        changePage(pageNumber) {
            this.page = pageNumber;
            this.fetchPosts();
        },

        async fetchPosts() {
            this.isPostsLoading = true;
            try{
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page:this.page,
                        _limit: this.limit,
                    }
                });
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
                this.posts = response.data;
                // console.log(response);
                this.isPostsLoading = false;
            }
            catch (err) {
                console.log('error');
            }
            
        }
    },

    mounted() {
        this.fetchPosts();
    },

    computed: {
        sortedSort() {
            return [...this.posts].sort((postA, postB) => {
                console.log(postA[this.selectedSort])
                return postA[this.selectedSort]?.localeCompare(postB[this.selectedSort])
            });
        },

        filterAndSort() {
            return this.sortedSort.filter(post=>post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
        // deep:true,
    },

    // watch: {
    //     selectedSort(newValue) {
    //         this.posts.sort((postA, postB) => {
    //             return postA[newValue]?.localeCompare(postB[newValue])
    //         });
    //         // console.log(newValue)
    //     },
    //     // deep:true,
        
    // }
}
</script>
<style>
    
    .app__btns {
        display: flex;
        justify-content: space-between;
        margin: 10px 0;
    }
    .page__wrapper {
        display: flex;
        justify-content: center;
        padding: 5px;
        margin-top: 15px;
    }
    .page {
        border: 1px solid black;
        margin-right: 20px;
        padding: 10px;
    }
    .current-page {
        border:2px solid red;
    }
</style>
