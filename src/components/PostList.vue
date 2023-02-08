<template>
    <div 
        v-if="POSTS.length > 0">
        <h3>Список Постов</h3>

        <transition-group name="post-list">
            <post-item
            v-for="post in POSTS"
            :post="post"
            :key="post.id"
            @remove= "$emit('remove', post)"
            />
        </transition-group>
    </div>
    <h2 v-else style="color: red">
        Список постов пуст
    </h2>
</template>
<script>
import PostItem from "@/components/PostItem.vue"
export default {
        components: {
            PostItem
        },
    props: {
        POSTS: {
            type: Array,
            required: true,
        }
    },
    
}
</script>
<style scoped>
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active, .post-list-leave-active {
  transition: all 0.3s;
}
.post-list-enter-from, .post-list-leave-to /* .list-leave-active до версии 2.1.8 */ {
  opacity: 0;
  transform: translateX(30px);
}
.post-list-move{
    transition: transform 1s;
}
</style>