<template>
    <div class="dialog" v-if="show" @click="hideDialog">
        <div class="dialog__content" @click.stop>
            <slot>

            </slot>
        </div>
    </div>
</template>
<script>
import toggleMixin from '@/mixin/toggleMixin';

export default {
    name: 'my-dialog',
    mixins: [toggleMixin]
    // props: {
    //     show: {
    //         type: Boolean,
    //         default: false,
    //     }
    // },
    // methods: {
    //     hideDialog() {
    //         this.$emit('update:show', false)
    //     }
    // }
}
</script>
<style>
    .dialog {
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
        background-color: rgba(0,0,0, 0.5);
        position: fixed;
        display: flex
    }
    .dialog__content{
        margin: auto;
        background-color: white;
        border-radius: 12px;
        padding: 15px;
        min-height: 50px;
        min-width: 300px;
    }
</style>