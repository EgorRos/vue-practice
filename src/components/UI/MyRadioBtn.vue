<template>
    <div 
        v-for="option of options"   
    >
        <input 
        @input="changeOption"
        :key="options.value" 
        type="radio"
        
        id="{{option.value}}"
        :value="option.value">
        <label for="{{ option.value }}">{{ option.name }}</label>
    </div>
</template>
<script>


export default {
    name: 'my-radio',
    props: {
        modelValue: {
            type: String,
        },
        options: {
            type: Array,
            default: () => []
        },
        def: {
            type: String,
        }
    },
    methods: {
        changeOption(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>
<style>

    
</style>