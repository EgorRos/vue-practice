<template>
    <div>
        <select 
        :value="modelValue" 
        @change="changeOption"
        >
            <option
                disabled 
                value=""
                >Выберете сортировку</option>
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
import { def } from '@vue/shared';

export default {
    name: 'my-select',
    props: {
        modelValue: {
            type: String
        },
        // option: {
        //     type: String,
        //     required: true,
        // },
        options: {
            type: Array,
            default: () => []
        },
        // def: {
        //     type: String,
        // }
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