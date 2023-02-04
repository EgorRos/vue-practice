<template>
    <div class='app'>
        <h1>Страница с постами</h1>
        <my-input v-model="searchQuery" placeholder="Поиск по названию..">
            
        </my-input>
        <div class="app__btns">
            <my-button
                @click="showDialog">Создание постов
            </my-button>
            <my-select
            v-model="selectedSort"
            :options="sortOptions"
            />
        </div>
        <my-dialog v-model:show="dialogVisible">
            <post-form
            @create="createPost"
        />
        </my-dialog>
        <post-list 
            :POSTS="sortedAndSearchedPosts"
            @remove="removePost"
            v-if="!isPostLoading"
        />
        <div v-else>Идет загрузка...</div>
        <!-- <div class="page__wrapper">
            <div 
            v-for="_page in totalPages" 
            :key="page" 
            class="page"
            :class="{ 
                'current-page': page == _page
            }"
            @click="changePage(_page)"
            >{{ _page }}</div>
        </div> -->

        <my-pages
            :totalPages="totalPages"
            :page="page"
            @changePage="changePage"
        />

        <cookies
            @submitCookies="submitCookies"
        />
        
    </div>
</template>

<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';
import Cookies from '@/components/sbmtCks.vue';
import axios from 'axios';
export default {
    components: {
        PostForm, PostList, Cookies
    },
    data() {
        return {
            posts: [], 
            dialogVisible: false,
            isPostLoading: false,
            selectedSort: '',
            sortOptions: [
                {value: 'title', name: 'По названию'},
                {value: 'body', name: 'По содержанию'},
                {value: 'id', name: 'По индексу'},
            ],
            searchQuery: '',
            page: 1,
            limit: 10,
            totalPages: 0,
        }
    },
    methods: {
        createPost(post){
            this.posts.push(post)
            this.dialogVisible = false;
            
        },
        removePost(post){
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        submitCookies() {
            alert("Спасибо за использование Cookies!")
        },
        showDialog() {
            this.dialogVisible = true
        },
        changePage(page) {
            this.page = page
        },
        async fetchPosts() { //Получение массива постов
            try {
                this.isPostLoading = true

                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
                this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)

                this.posts = response.data //помещение постов в posts

                this.isPostLoading = false


            } catch (e) {
                alert('Error')
            } finally {

            }

        }
    },
    mounted() {
        this.fetchPosts();
    }, 
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => {
                let total = 0
                if (this.selectedSort === "id") {
                    if (post1[this.selectedSort]<post2[this.selectedSort]) {
                        total = -1
                    } else if (post1[this.selectedSort]>post2[this.selectedSort]) {
                        total = 1
                    }
                } else {
                    total = post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
                }
                
                return total
            })
        },
        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLocaleLowerCase()))
        }
    },

    
    watch: {
        page() {
         this.fetchPosts()
        }

    //     selectedSort(newValue) {
    //         this.posts.sort((post1, post2) => {
    //             console.log(post1)
    //             console.log(newValue)
    //             return post1[newValue]?.localeCompare(post2[newValue])
    //         })
    //     }, //функция наблюдатель имеет такое же название, как и модель в компоненте
    }

}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app {
    padding: 20px;
}

.app__btns {
    display: flex;
    justify-content: space-between;
}
.page__wrapper {
    display: flex;
    margin-top: 15px;
}
.page {
    border: 2px solid teal;
    padding: 10px;
    margin: 0 5px;
}

.page:hover {
    cursor: pointer;
}

.current-page {
    border: 2px solid salmon;
}


</style>

