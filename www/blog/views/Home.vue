<template>
    <section class="section section-container">
        <div class="section-title">
            <h1>优秀的你，才能遇到优秀的世界<br />Bag管理系统框架</h1>
        </div>
        <div class="action">
            <el-row :gutter="30">
                <el-col :xs="24" :sm="24" :md="12" :lg="6" :xl="6">
                    <div class="demo">
                        <vs-button target :href="{url: '/admin.html'}" color="primary" size="large"
                                   type="filled" icon="text_snippet"
                        >体验管理端
                        </vs-button>
                    </div>
                </el-col>
                <el-col :xs="24" :sm="24" :md="12" :lg="6" :xl="6">
                    <div class="demo">
                        <vs-button target :href="{url: '/web.html'}" color="rgb(11, 189, 135)" size="large"
                                   type="filled"
                                   icon="text_snippet"
                        >体验客户端
                        </vs-button>
                    </div>
                </el-col>
                <el-col :xs="24" :sm="24" :md="12" :lg="6" :xl="6">
                    <div class="demo">
                        <vs-button target :href="{url: '/doc/index.html'}" color="danger" size="large"
                                   type="filled" icon="text_snippet"
                        >查看文档
                        </vs-button>
                    </div>
                </el-col>
                <el-col :xs="24" :sm="24" :md="12" :lg="6" :xl="6">
                    <div class="demo">
                        <vs-button color="success" @click="handleDownload" size="large" type="filled"
                                   icon="downloading"
                        >
                            下载程序
                        </vs-button>
                    </div>
                </el-col>
            </el-row>
        </div>
    </section>
</template>
<script lang="ts" setup>
import { browser } from 'pm-utils'

const handleDownload = () => {
    browser.smoothScroll('#Download')
}
</script>
<style lang="less" scoped>
.section {
    padding-top: 220px;
    padding-bottom: 220px;
    background: rgba(0, 0, 0, 0.5);
    position: relative;
    overflow: hidden;
    color: #FFFFFF;
    text-align: center;

    &-title {
        h1 {
            font-size: 50px;
            font-weight: bold;
        }
    }

    .action {
        width: 60%;
        margin: 80px auto 0;
    }

    .demo {
        margin-top: 30px;
        display: flex;
        justify-content: center;
    }
}
</style>
