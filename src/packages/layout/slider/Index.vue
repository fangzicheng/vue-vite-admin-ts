<template>
    <a-layout-sider theme="light" :width="compData.width" v-model:collapsed="compData.collapsed" collapsible>
        <div class="logo">{{ compData.collapsed ? compData.subhead : compData.title }}</div>
        <div class="scroll">
            <MenuSlider />
        </div>
    </a-layout-sider>
</template>
<script lang="ts">
import { computed, defineComponent, reactive } from 'vue'
import appPinia from '@/packages/pinia/app'
import MenuSlider from './MenuSlider'

export default defineComponent({
    name: 'Slider',
    components: {
        MenuSlider,
    },
    setup() {
        const appStore = appPinia()
        const { title, subhead } = appStore.configApp.webSite
        const compData = reactive({
            title,
            collapsed: computed(() => appStore.bagConfig.collapsed),
            width: 0,
            subhead,
        })
        compData.width = compData.collapsed ? 80 : 250
        return {
            compData,
        }
    },
})
</script>
<style lang="less" scoped>
.logo {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 80px;
    cursor: pointer;
    background-color: #2f3447;
    color: #ffffff;
    font-size: 25px;
    font-weight: bold;
}

.scroll {
    overflow-y: scroll;
    height: calc(100% - 80px);
}
</style>
