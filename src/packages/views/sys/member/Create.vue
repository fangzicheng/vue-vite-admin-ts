<template>
    <div>
        <a-form ref="formRef" :model="formState" :rules="rules" :label-col="{span: 6}" :wrapper-col="{ span: 15}">
            <a-row>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="部门组织" name="did">
                        <a-tree-select
                            v-model:value="formState.did"
                            style="width: 100%"
                            :dropdown-style="{ maxHeight: '400px', overflow: 'auto' }"
                            :tree-data="treeData"
                            :field-names="{children:'children', key:'id', value: 'id', label: 'name'}"
                            placeholder="选择部门组织"
                            allow-clear
                            tree-default-expand-all
                        >
                        </a-tree-select>
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="角色" name="roles">
                        <a-select
                            v-model:value="formState.roles"
                            style="width: 100%"
                            placeholder="选择用户角色"
                        >
                            <a-select-option v-for="item in rolesOptions" :key="item.id" :value="item.id">{{item.tag}}</a-select-option>
                        </a-select>
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="姓名" name="username">
                        <a-input v-model:value="formState.username" placeholder="输入用户姓名" />
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="性别" name="sex">
                        <a-select
                            v-model:value="formState.sex"
                            style="width: 100%"
                            placeholder="选择用户性别"
                        >
                            <a-select-option :value="1">女</a-select-option>
                            <a-select-option :value="2">男</a-select-option>
                            <a-select-option :value="0">保密</a-select-option>
                        </a-select>
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="年龄" name="age">
                        <a-input v-model:value="formState.age" placeholder="输入年龄" />
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="邮箱" name="email">
                        <a-input v-model:value="formState.email" placeholder="输入邮箱" />
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="手机号" name="phone">
                        <a-input v-model:value="formState.phone" placeholder="输入手机号" />
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="职业" name="job">
                        <a-input v-model:value="formState.job" placeholder="输入职业" />
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="出生年月" name="birthday">
                        <a-input v-model:value="formState.birthday" placeholder="输入出生年月" />
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="公司名称" name="company">
                        <a-input v-model:value="formState.company" placeholder="输入公司名称" />
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="地址" name="address">
                        <a-input v-model:value="formState.address" placeholder="输入地址" />
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="擅长编程语言" name="software">
                        <a-input v-model:value="formState.software" placeholder="输入擅长编程语言" />
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="是否禁用" name="state">
                        <a-radio-group v-model:value="formState.state">
                            <a-radio :value="1">启用</a-radio>
                            <a-radio :value="0">禁用</a-radio>
                        </a-radio-group>
                    </a-form-item>
                </a-col>
                <a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                    <a-form-item label="描述" name="describe">
                        <a-textarea v-model:value="formState.describe" placeholder="输入描述" />
                    </a-form-item>
                </a-col>
            </a-row>
        </a-form>
    </div>
</template>
<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import { apiAll as apiBranchAll } from '@/packages/service/branch'
import { toTree } from '@/packages/utils/utils'
import { validatPhone } from '@/packages/utils/validator'
import { apiAll as apiRoleAll } from '@/packages/service/role'

export default defineComponent({
    setup() {
        const treeData = ref()
        const rolesOptions = ref()
        const formRef = ref()
        const formState: any = reactive({
            username: '',
            sex: 1,
            age: '',
            email: '',
            phone: '',
            roles: [],
            describe: '',
            did: undefined,
            state: 1,
            job:'',
            birthday:'',
            company:'',
            address:'',
            software:''
        })
        const rules = {
            username: [
                { required: true, message: '姓名为必填项', trigger: 'blur' },
            ],
            phone: [
                { required: true, validator: validatPhone, trigger: 'blur' },
            ],
            describe: [
                { trigger: 'blur', max: 200, message: '最大长度为200' },
            ],
        }
        apiBranchAll().then((res: any) => {
            treeData.value = toTree(res);
        })
        apiRoleAll().then((res: any) => {
            rolesOptions.value = res;
        })
        return {
            formState,
            rules,
            treeData,
            rolesOptions,
            formRef,
        }
    },
})
</script>
<style lang="less" scoped>
.item-icons {
    .item {
        text-align: center;
        padding: 10px 0;
        cursor: pointer;
        font-size: 20px;
        display: flex;
        align-items: center;
        justify-content: center;

        &-icon {
            border: 1px solid #ddd;
            width: 45px;
            border-radius: 3px;
        }
    }
}
</style>
