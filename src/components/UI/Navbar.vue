<template>
    <div class="navbar">
        <div @click="$router.push('/')"
        >Vue 3 test app</div>
        <div class="navbar__btns">
            <my-button
             @click="$router.push('/posts')"
             >Посты</my-button>
            <my-button 
            @click="$router.push('/about')"
            >О сайте</my-button>

        </div>
    </div>
</template>
<script>
export default {
    
}
</script>
<style>
    .navbar {
        height: 50px;
        background-color: lightgray;
        box-shadow: 2px 2px 4px gray;
        display: flex;
        align-items: center;
        
    }
    .navbar__btns{
        display: flex;
        flex-direction: row;
        text-decoration: none;
        gap: 10px;
        margin-left: auto;
    }
    
</style>