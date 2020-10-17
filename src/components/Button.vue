<template>
    <button class="button" @click="$emit('click',$event)">
        <slot></slot>
    </button>
</template>

<script>
    import Vue from 'vue'
    import {Component} from 'vue-property-decorator'

    @Component
    export default class Button extends Vue {

    }


</script>

<style lang="scss" scoped>
    .button {
        background: #767676;
        color: #fff;
        border-radius: 4px;
        border: none;
        height: 44px;
        padding: 0 16px;

        &-wrapper {
            text-align: center;
            padding: 16px;
            margin-top: 28px;
        }
    }
</style>