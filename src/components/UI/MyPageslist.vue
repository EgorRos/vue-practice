<template>
    <div class="page__wrapper">
            <div 
            v-for="_page in totalPages" 
            :key="page" 
            class="page"
            :class="{ 
                'current-page': page == _page
            }"
            @click="$emit('changePage', _page) "
            >{{ _page }}</div>
        </div>
</template>
<script>
import { numberLiteralTypeAnnotation } from '@babel/types';

export default {
    name: 'my-pages',
    props: {
        page: {
            type: Number,
            required: true,
        },
        totalPages: {
            type: Number,
            required: true,
        }
    },
}
</script>
<style>
    
.page__wrapper {
    display: flex;
    margin-top: 15px;
}
.page {
    border: 2px solid teal;
    padding: 10px;
    margin: 0 5px;
}

.page:hover {
    cursor: pointer;
}

.current-page {
    border: 2px solid salmon;
}
</style>