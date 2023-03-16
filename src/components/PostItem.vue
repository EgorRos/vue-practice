<template>
    <div class="post">
        <div>
            <div><strong>id</strong> {{ post.id }} </div>
            <div><strong>Название</strong> {{ post.title }} </div>
            <div><strong>описание</strong> {{ post.body }} </div>

        </div>
        <div class="post__btns">
            <my-button @click="$router.push(`/posts/${post.id}`)"
            >Открыть
            </my-button>
            <my-button
                @click = "$emit('remove', post)"
            > Удалить </my-button> 
        </div>

    </div>
</template>
<script>

export default {

    props: {
        post: {
            type: Object,
            required: true,
        }
    },
}
</script>
<style scoped>
    .post {
    padding: 15px;
    border: 2px solid teal;
    margin: 15px 0 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
    .post__btns{
        display: flex;
    }
</style>