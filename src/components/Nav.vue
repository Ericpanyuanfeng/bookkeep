<template>
    <nav>
        <router-link to="/money" class="item" active-class="selected">
            <Icon name="money"/>
            记账
        </router-link>

        <router-link to="/labels" class="item" active-class="selected">
            <Icon name="label"/>
            标签
        </router-link>

        <router-link to="/statistics" class="item" active-class="selected">
            <Icon name="statistics"/>
            统计
        </router-link>

    </nav>
</template>

<script lang="ts">
    const importAll = (requireContext: __WebpackModuleApi.RequireContext) => requireContext.keys().forEach(requireContext);
    try {
        importAll(require.context('../assets/icons', true, /\.svg$/));
    } catch (error) {
        console.log(error);
    }


    export default {
        name: 'Nav'
    };
</script>

<style lang="scss" scoped>
    @import "~@/assets/style/helper.scss";

    nav {
        @extend %outerShadow;
        display: flex;
        font-size: 12px;

        > .item {
            width: 33.3333333333%;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            padding: 2px 0;

            .icon {
                width: 32px;
                height: 32px;
            }
        }

        > .item.selected {
            color: #dc3023;
        }
    }
</style>