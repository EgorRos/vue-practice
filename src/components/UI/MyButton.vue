<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>

<script>
export default {
    name: 'my-button'
}
</script>

<style>
.btn {
    display: flex;
    align-self: flex-end;
    padding: 10px;
    background: none;
    color: teal;
    border: solid 2px teal;
}

.btn:hover{
    background-color: aliceblue;
}

.btn:active{
    background-color: lightskyblue;
    border: 2px solid black;
}
</style>