<template>
  <div class="login_container">
    <div class="login_box">
      <!--头像区-->
      <div class="avatar_box">
        <img src="../assets/logo.png" alt />
      </div>
      <!--表单区-->
      <el-form ref="loginFormRef"  :model="loginForm" :rules="loginFormRules" label-width="0px" class="login_form" >
        <!--USERNAME-->
        <el-form-item prop="username">
          <el-input v-model="loginForm.username" prefix-icon="iconfont icon-user"></el-input>
        </el-form-item>
        <!--PASSWORD-->
        <el-form-item prop="password">
          <el-input v-model="loginForm.password" prefix-icon="iconfont icon-passord" type="password"></el-input>
        </el-form-item>
        <!--BUTTON-->
        <el-form-item class="btn">
          <el-button type="primary" @click="login">登录</el-button>
          <el-button type="info" @click="resetLoginForm">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      // 这是登录表单的数据对象
      loginForm: {
        username: '',
        password: ''
      },
      // 表单数据验证
      loginFormRules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入登录密码', trigger: 'blur' },
          { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    resetLoginForm () {
      // console.log(this)
      this.$refs.loginFormRef.resetFields()
    },
    // 表单的预验证
    login () {
      this.$refs.loginFormRef.validate(async (valid) => {
        // eslint-disable-next-line no-useless-return
        if (!valid) return
        // const result = this.$http.post('login', this.loginForm)
        const { data: ret } = await this.$http.get('http://127.0.0.1:8088/account/login/')
        console.log(ret)
        if (ret.status === 200) return this.$message.success('登录成功')
      })
    }
  }
}
</script>

<style lang="less" scoped>
.login_container {
  background-color: #2b4b6b;
  height: 100%;
}

.login_box {
  width: 450PX;
  height: 400PX;
  background-color: #fff;
  border-radius: 25px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
// 头像样式设置
.avatar_box {
  height: 130px;
  width: 130px;
  border: 1px solid #eee;
  border-radius: 50%;
  padding: 10px;
  box-shadow: 0 0 10px #ddd;
  position: absolute;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  img {
    height: 130px;
    width: 130px;
    border-radius: 50%;
    background-color: #eee;
  }
}
.btn {
  display: flex;
  justify-content: flex-end;
}
.login_form {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}
</style>
