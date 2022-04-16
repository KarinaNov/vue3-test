<template>
    <div>
        <h1>{{ $store.state.post.limit }}</h1>
        <!-- <h1>Страница с постами</h1>
        <my-input
            v-focus
            v-model="searchQuery"
            placeholder="Поиск..."
        />
        <div class="app__btns">
            <my-button
                @click="showDialog"
            >Создать пост
            </my-button>
            <my-select
                v-model="selectedSort"
                :options="sortOption"
            />
        </div>
       
        <my-dialog v-model:show="dialogVisible">
            <post-form 
                @create="createPost"
            />
        </my-dialog>
        <post-list 
            :posts="sortedAndSearchesPosts"
            @remove="removePost"
            v-if="!isPostLoading"    
        />
        <div v-else>Идет загрузка...</div>
        <div v-intersection="loadMorePosts" class="observer"></div> -->
        <!-- <div class="page__wrapper">
            <div 
                v-for="pageNumber in totalPages"
                :key="pageNumber"
                class="page"
                :class="{
                    'current-page': page === pageNumber
                }"
                @click="changePage(pageNumber)"
            >
            {{ pageNumber }}
            </div>
        </div> -->
    </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyButton from "@/components/UI/MyButton";
import MyDialog from "@/components/UI/MyDialog";
import axios from 'axios'
import MySelect from "@/components/UI/MySelect";
import MyInput from "@/components/UI/MyInput";

export default {
    components: {
        PostList, 
        PostForm,
        MyDialog,
        MyButton,
        MySelect,
        MyInput
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostLoading: false,
            selectedSort: '',
            searchQuery: '',
            page: 1,
            limit: 10,
            totalPages: 0,
            sortOption: [
                {value: 'title', name: 'По названию'},
                {value: 'body', name: 'По содержимому'}
            ]
        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post){
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog(){
            this.dialogVisible = true
        },
        // changePage(pageNumber){
        //     this.page = pageNumber
        // },
        
    },
    mounted(){
        this.fetchPosts();
        // const options = {
        //     rootMargin: '0px',
        //     threshold: 1.0
        // }
        // const callback = (entries, observer) => {
        //     if(entries[0].isIntersecting && this.page < this.totalPages){
        //         this.loadMorePosts()
        //     }
        // };
        // const observer = new IntersectionObserver(callback, options);
        //    observer.observe(this.$refs.observer)
        },
    computed: {
        
    },
    watch: {
        // page(){
        //     this.fetchPosts()
        // }
    }
}

</script>

<style scoped>
.app__btns{
    display: flex;
    justify-content: space-between;
    margin: 0 15px;
}
.page__wrapper{
    display: flex;
    margin-top: 15px;
}
.page{
    border: 1px solid black;
    padding: 10px;
}
.current-page{
    border: 2px solid teal;
}
</style>