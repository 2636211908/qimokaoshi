<template>
 <div class="">
  <el-card>
    <el-icon :size="56" color="#409eff">
      <Shop></Shop>
    </el-icon>
    <h2>mall-admin-app</h2>

    <el-form
    ref="ruleFormRef"
    style="max-width: 600px"
    :model="ruleForm"
    :rules="rules"
    label-width="auto"
    class="demo-ruleForm"
    :size="formSize"
    status-icon
  >
    <el-form-item prop="username">
      <el-input
      v-model="ruleForm.username"
      style="width: 240px"
      :prefix-icon="User"
    />
    </el-form-item>
    <el-form-item prop="password">
      <el-input
      v-model="ruleForm.password"
      style="width: 240px"
      placeholder="请输入密码"
      show-password
      :prefix-icon="Lock"
    />
    </el-form-item>
    <el-form-item>
      
      <el-button type="primary" @click="submitForm(ruleFormRef)">
        登录
      </el-button>
    </el-form-item>
  </el-form>
  </el-card>
</div>
</template>
<script setup lang="ts">
import {ref,reactive} from "vue"
import type { ComponentSize, FormInstance, FormRules } from 'element-plus'
import {User , Lock} from "@element-plus/icons-vue"
 
interface RuleForm {
  username: string
  password: string
}
const formSize = ref<ComponentSize>('default')
const ruleFormRef = ref<FormInstance>()
const ruleForm = reactive<RuleForm>({
  username: 'admin',
  password: ''
})

const rules = reactive<FormRules<RuleForm>>({
  username: [
    { required: true, message: '请输入正确的用户名', trigger: 'blur' },
  ],
  password: [
    { required: true, message: '请输入密码', trigger: 'blur' },
    { min: 3, max: 8, message: '密码不能小于3位', trigger: 'blur' },
  ]
})


const submitForm = async (formEl: FormInstance | undefined) => {
  if (!formEl) return
  await formEl.validate((valid, fields) => {
    if (valid) {
      console.log('submit!')
    } else {
      console.log('error submit!', fields)
    }
  })
}

</script>
<style lang="scss" scoped>
.el-card{
  width: 320px;
  height: 400px;
  margin: 150px auto;
  display: flex;
  justify-content: space-evenly;
  .el-icon svg{
    margin-right: -140px;
  }
  h2{
    color: #409eff;
  }
}
</style>
