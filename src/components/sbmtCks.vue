<template>
    <div>
        <my-button class="cookies-btn"
                @click="submitCookies"
            > Принять использование Cookies</my-button>
    </div>
</template>
<script>
export default {
    methods: {
        submitCookies() {
            this.$emit('submitCookies')
        }
    }
}
</script>
<style>
.cookies-btn{
    margin: 10px 0;
}
</style>