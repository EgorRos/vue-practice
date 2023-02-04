<template lang="">
    <input 
    :value="modelValue" 
    @input="updateInput" 
    class="input" 
    type="text">
</template>


<script>
export default {
    name: "my-input",
    props: {
        modelValue: [String, Number]
    },
    methods: {
        updateInput(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>


<style scoped>
    form{
    display: flex;
    flex-direction: column;
}
.input{
    width: 100%;
    border: 2px solid salmon;
    padding: 10px 15px;
    margin: 15px 0 0;
}
</style>