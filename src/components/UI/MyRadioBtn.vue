<template>
    <div 
    v-for="option of options"   
        :key="options.value"
    >
        <input 
        type="radio"
        :name="groupName"
        :id="option.value"
        :value="option.value"
        :checked="defaultOption === option.value"
        @change="$emit('update:modelValue', option.value)"
        >
        <label :for="option.value">{{ option.name }}</label>
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
        defaultOption: {
            type: String,
        },
        groupName: {
            type: String
        }
    },

    // methods: {
    //     changeOption(event) {
    //         this.$emit('update:modelValue', event.target.value)
    //     }
    // },
    // mounted() {
        
    // },
    // @input="changeOption"
        
    //     type="radio"
    //     :name="groupName"
    //     :id="option.value"
    //     :value="option.value"

    // :for="option.value">{{ option.name }}
}
</script>


<style>

</style>