<template>
    <div>
        <select 
        :value="modelValue" 
        @change="changeOption"
        >
            <option disabled value="">Выберете из списка</option>
            <option 
            v-for="option of options" 
            :key="options.value" 
            :value="option.value"
        >
            {{ option.name }}
            </option>
        </select>
    </div>
</template>
<script>
export default {
    name: 'my-select',
    props: {
        modelValue: {
            type: String
        },
        options: {
            type: Array,
            default: () => []
            
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