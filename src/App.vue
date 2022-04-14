<template>
  <a-form-model ref="ruleForm" :model="ruleForm" :rules="rules" v-bind="layout">
    <h1>Welcome Back!</h1>
    <hr>
    <a-form-model-item has-feedback label="Email" prop="mail">
      <a-input v-model="ruleForm.mail" type="text" autocomplete="off" />
    </a-form-model-item>
    <a-form-model-item has-feedback label="Mật khẩu" prop="checkPass">
      <a-input v-model="ruleForm.checkPass" type="password" autocomplete="off" />
    </a-form-model-item>
    <a-form-model-item :wrapper-col="{ span: 14, offset: 4 }">
      <a-radio>Ghi nhớ đăng nhập</a-radio> <br>
      <a href="">Tạo tài khoản mới</a> <br>
      <a href="">Quên mật khẩu</a> <br>
      <a-button type="primary" @click="submitForm('ruleForm')">
        Đăng nhập
      </a-button>
    </a-form-model-item>
  </a-form-model>
</template>
<script>
export default {
  data () {
    // eslint-disable-next-line
    const fillter = /^([a-zA-Z0-9_\.\-])+\@(([a-zA-Z0-9\-])+\.)+([a-zA-Z0-9]{2,4})+$/
    const validateMail = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('Vui lòng nhập Email'))
      } if (!fillter.test(value)) {
        callback(new Error('Vui lòng nhập Email hợp lệ'))
        return false
      }
      callback()
    }
    // eslint-disable-next-line
    const truePw = /^(?=.*[~`!@#$%^&*()--+={}\[\]|\\:;"'<>,.?/_₹])/
    const validatePass = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('Vui lòng nhập mật khẩu'))
      } if (!truePw.test(value)) {
        callback(new Error('Mật khẩu không đủ mạnh'))
      } callback()
    }
    return {
      ruleForm: {
        mail: '',
        checkPass: ''
      },
      rules: {
        mail: [{ validator: validateMail, trigger: 'change' }],
        checkPass: [
          {
            min: 8,
            trigger: 'change',
            message: 'Mật khẩu có ít nhất 8 kí tự'
          },
          {
            validator: validatePass,
            trigger: 'change'
          }
        ]
      },
      layout: {
        labelCol: { span: 4 },
        wrapperCol: { span: 8 }
      }
    }
  },
  methods: {
    submitForm (formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert('submit!')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    resetForm (formName) {
      this.$refs[formName].resetFields()
    }
  }
}
</script>

<style scoped>
h1 {
  text-align: center;
}
hr {
  display: block;
  margin-top: 0.5em;
  margin-bottom: 0.5em;
  margin-left: auto;
  margin-right: auto;
  border-style: inset;
  border-width: 1px;
  width: 100px;
}
a:hover {
  color: darkred;
}
</style>
