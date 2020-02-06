<template>
  <div class="container">
    <el-card class="my-card">
      <img src="../../assets/logo_index.png" />
      <el-form :model="form" :rules="rules" ref="myFrom" status-icon>
        <el-form-item prop="mobile">
          <el-input v-model="form.mobile" placeholder="请输入手机号"></el-input>
        </el-form-item>

        <el-form-item prop="code">
          <el-input v-model="form.code" placeholder="请输入验证码" style="width:240px;margin-right:8px"></el-input>
          <el-button>发送验证码</el-button>
        </el-form-item>

        <el-form-item>
          <el-checkbox :value="true">我已阅读并同意用户协议和隐私条款</el-checkbox>
        </el-form-item>

        <el-form-item>
          <el-button type="primary" style="width:100%" @click="login()">登录</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    const checkMoblie = (rules, value, callback) => {
      if (!/^1[3-9]\d{9}$/.test(value)) {
        callback(new Error('输入正确的手机号'))
      } else {
        callback()
      }
    }

    return {
      form: {
        mobile: '',
        code: ''
      },
      rules: {
        mobile: [{
          required: true,
          message: '输入正确的手机号',
          trigger: 'blur'
        }, {
          validator: checkMoblie,
          trigger: 'blur'
        }],
        code: [{
          required: true,
          message: '输入正确的验证码',
          trigger: 'blur'
        }, {
          len: 6,
          message: '验证码为6位',
          trigger: 'blur'
        }]
      }
    }
  },
  methods: {
    login () {
      this.$refs.myFrom.validate((valid) => {
        if (valid) {}
      })
    }
  }
}
</script>

<style lang='less'>
.container {
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  position: absolute;
  background: url(../../assets/login_bg.jpg);
  background-size: cover;
  .my-card {
    width: 400px;
    height: 350px;
    position: absolute;
    transform: translate(-50%, -60%);
    left: 50%;
    top: 50%;
    img {
      width: 200px;
      display: block;
      margin: 0 auto 20px;
    }
  }
}
</style>
