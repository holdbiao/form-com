<template>
  <div id="app">
    <biu-form :model="form" :rules="rules" ref="loginFrom">
      <biu-form-item label="账户" prop="user">
        <biu-input v-model="form.user" placeholder="请输入账号"></biu-input>
      </biu-form-item>
      <biu-form-item label="密码" prop="password">
        <biu-input type="password" v-model="form.password" placeholder="请输入密码"></biu-input>
      </biu-form-item>
    </biu-form>
    <button @click="login">登陆</button>
    <p>{{form}}</p>
  </div>
</template>

<script>
import BiuInput from './components/form/BiuInput'
import BiuFormItem from './components/form/BiuFormItem'
import BiuForm from './components/form/BiuForm'

export default {
  name: 'app',
  components: {
    BiuInput, BiuFormItem, BiuForm
  },
  data () {
    return {
      form: {
        user: '12',
        password: ''
      },
      rules: { // 校验规则，同element-ui
        user: [
          {required: true, message: '请输入账户'}
        ],
        password: [
          {required: true, message: '请输入密码'}
        ]
      }
    }
  },
  methods: {
    login () {
      this.$refs.loginFrom.validate(isValidate => {
        if (isValidate) {
          console.log('pass')
          console.log(isValidate)
        } else {
          console.log('fail')
        }
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
