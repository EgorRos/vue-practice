<template>
    <div class='app'>
        <h1>Страница с постами</h1>
        <my-input v-model="searchQuery" placeholder="Поиск по названию..">
            
        </my-input>
        <div class="app__btns">
            <my-button
                @click="showDialog">Создание постов
            </my-button>
            <my-radio
            v-model="selectedPagination"
            :options="paginationOptions"
            :def="paginationOptions[0].value"
            />
            <my-select
            v-model="selectedSort"
            :options="sortOptions"
            />
            <!-- @change-option="optionChanged" -->
        </div>
        <my-dialog v-model:show="dialogVisible">
            <post-form
            @create="createPost"
        />
        </my-dialog>
        <post-list 
            :POSTS="postsShowed"
            @remove="removePost"
            v-if="!isPostLoading"
        />
        <div v-else>Идет загрузка...</div>

        <!-- <div 
            v-if="selectedPagination=='endlessList'"
            ref="observer" 
            class="observer"
        ></div> -->

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

        <!-- <cookies
            @submitCookies="submitCookies"
        /> -->
        
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
            postsShowed: [],
            dialogVisible: false,
            isPostLoading: false,
            selectedSort: '',
            sortOptions: [
                {value: 'title', name: 'По названию'},
                {value: 'body', name: 'По содержанию'},
                {value: 'id', name: 'По индексу'},
            ],
            selectedPagination: '',
            paginationOptions: [
                {value: 'pages', name: 'Постранично'},
                {value: 'endlessList', name: 'Бесконечный список'},
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
        // optionChanged() {
        //     this.page = 1;
        // },
        async fetchPosts() { //Получение массива постов
            try {
                this.isPostLoading = true

                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts'
                    // , {
                    //     params: {
                    //     _limit : this.limit,
                    //     _page : this.page
                        
                    //     }}
                        )
                
                this.totalPages = Math.ceil(response.data.length / this.limit)
                

                this.posts = response.data //помещение постов в posts

                this.isPostLoading = false


            } catch (e) {
                alert('Error')
            } finally {

            }

        }
    },
    mounted() {
        this.fetchPosts()
        const options = {

        rootMargin: '0px',
        threshold: 1.0
        }
            const callback = (entries, observer) => {
                if (entries[0].isIntersecting) {
                    this.limit += 10
                }
        }
            const observer = new IntersectionObserver(callback, options)
            observer.observe(this.$refs.observer)
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
        },
        postsShowed() {
            return this.sortedAndSearchedPosts.slice(this.page*this.limit-this.limit, this.page*this.limit)
        },
    },

    
    watch: {
        // page() {
        //  this.fetchPosts()
        // },
        selectedSort() {
            this.page = 1;
        },

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

