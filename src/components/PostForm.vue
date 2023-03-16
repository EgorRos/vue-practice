<template>
    <form @submit.prevent>
            <h4>Создание поста</h4>
            <my-input
            v-focus
            v-model="post.title"
            class='input' 
            type="text" 
            placeholder="Название поста" 
            name="" id=""/>
            <my-input 
            v-model="post.body"
            class='input' 
            type="text"
            placeholder="Содержание поста" 
            name="" id=""/>
            <my-button
                @click="createPost"
            > Создать</my-button>
        </form>
</template>
<script>
export default {
    data() {
        return {
            post: {
                title: '',
                body: '',
            }
        }
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            this.$emit('create', this.post);
            this.post = {
                title: '',
                body: '',
            };
        }
    },
    watch: {
        post: {
            handler(newValue){
                console.log(newValue)
            },
            deep: true
        } //функция наблюдатель с глубоким отслеживанием (если делать без него будет работать только на создание объекта)
    }
    
}
</script>
<style scoped>


.btn{
    margin: 15px 0 0;
}

</style>