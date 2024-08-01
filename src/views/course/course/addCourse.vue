<template>
  <div>
    <el-form ref="formRef" :model="formData" :rules="rules" size="default" label-width="100px">
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="课程编号" prop="courseNumber">
            <el-input v-model="formData.courseNumber" type="text" placeholder="请输入课程编号" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="课程学科" prop="subject">
            <el-input v-model="formData.subject" type="text" placeholder="请输入课程学科" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="课程名称" prop="courseName">
            <el-input v-model="formData.courseName" type="text" placeholder="请输入课程名称" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="课程价格" prop="coursePrice">
            <el-input v-model="formData.coursePrice" type="text" placeholder="请输入课程价格" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="适用人群" prop="orientPeople">
            <el-input v-model="formData.orientPeople" type="text" placeholder="请输入适用人群" clearable
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="有效时间" prop="validTime">
            <el-time-picker v-model="formData.validTime" is-range format="HH:mm:ss" value-format="HH:mm:ss"
              :style="{width: '100%'}" start-placeholder="开始时间" end-placeholder="结束时间" range-separator="至"
              clearable></el-time-picker>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="12">
          <el-form-item label="课程封面" prop="courseCover" required>
            <el-upload ref="courseCover" :file-list="courseCoverfileList" :action="courseCoverAction"
              :before-upload="courseCoverBeforeUpload">
              <el-button size="small" type="primary" icon="el-icon-upload">点击上传</el-button>
            </el-upload>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="推荐指数" prop="recommandIndex">
            <el-rate v-model="formData.recommandIndex"></el-rate>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row gutter="15">
        <el-col :span="18">
          <el-form-item label="课程介绍" prop="field115">
            <el-input v-model="formData.field115" type="textarea" placeholder="请输入课程介绍"
              :autosize="{minRows: 4, maxRows: 4}" :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-form-item>
        <el-button type="primary" @click="submitForm">提交</el-button>
        <el-button @click="resetForm">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script setup>
import {
  ElMessage
}
from 'element-plus'
const formRef = ref()
const data = reactive({
  formData: {
    courseNumber: undefined,
    subject: undefined,
    courseName: undefined,
    coursePrice: undefined,
    orientPeople: undefined,
    validTime: null,
    courseCover: null,
    recommandIndex: 0,
    field115: undefined,
  },
  rules: {
    courseNumber: [{
      required: true,
      message: '请输入课程编号',
      trigger: 'blur'
    }],
    subject: [{
      required: true,
      message: '请输入课程学科',
      trigger: 'blur'
    }],
    courseName: [{
      required: true,
      message: '请输入课程名称',
      trigger: 'blur'
    }],
    coursePrice: [{
      required: true,
      message: '请输入课程价格',
      trigger: 'blur'
    }],
    orientPeople: [{
      required: true,
      message: '请输入适用人群',
      trigger: 'blur'
    }],
    validTime: [{
      required: true,
      message: '有效时间不能为空',
      trigger: 'change'
    }],
    recommandIndex: [{
      required: true,
      message: '推荐指数不能为空',
      trigger: 'change'
    }],
    field115: [{
      required: true,
      message: '请输入课程介绍',
      trigger: 'blur'
    }],
  }
})
const {
  formData,
  rules
} = toRefs(data)
// 上传请求路径
const courseCoverAction = ref('https://jsonplaceholder.typicode.com/posts/')
// 上传文件列表
const courseCoverfileList = ref([])
/**
 * @name: 上传之前的文件判断
 * @description: 上传之前的文件判断，判断文件大小文件类型等
 * @param {*} file
 * @return {*}
 */
function courseCoverBeforeUpload(file) {
  let isRightSize = file.size / 1024 / 1024 < 2
  if (!isRightSize) {
    ElMessage.error('文件大小超过 2MB')
  }
  return isRightSize
}
/**
 * @name: 表单提交
 * @description: 表单提交方法
 * @return {*}
 */
function submitForm() {
  formRef.value.validate((valid) => {
    if (!valid) return
    // TODO 提交表单
  })
}
/**
 * @name: 表单重置
 * @description: 表单重置方法
 * @return {*}
 */
function resetForm() {
  formRef.value.resetFields()
}

</script>
<style>
.el-upload__tip {
  line-height: 1.2;
}

.el-rate {
  display: inline-block;
  vertical-align: text-top;
}

</style>
