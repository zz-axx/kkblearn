<template>
  <section class="index">
    <KForm :model="model" :rules="rules" ref="loginForm">
      <KFormItem label="用户名" prop="username">
        <KLinput v-model="model.username" placeholder="请输入内容"></KLinput>
      </KFormItem>
      <KFormItem label="密码" prop="password">
        <KLinput
          type="password"
          v-model="model.password"
          placeholder="请输入密码"
        ></KLinput>
      </KFormItem>
      <KFormItem>
        <button @click="onLogin">登录</button>
      </KFormItem>
    </KForm>
  </section>
</template>

<script>
import KFormItem from './KFormItem.vue'
import KLinput from './KInput'
import KForm from './KForm'
export default {
  name: 'index',
  data () {
    return {
      model: {
        username: 'temp',
        password: ''
      },
      rules: {
        username: [{ required: true, message: '用户名为必填项！' }],
        password: [{ required: true, message: '密码为必填项！' }]
      }
    }
  },
  components: {
    KLinput,
    KFormItem,
    KForm
  },
  watch: {},
  mounted () {},
  methods: {
    onLogin () {
        console.log("onLOgin")
      this.$refs.loginForm.validate(isValid => {
          console.log("isValid",isValid)
        if (isValid) {
          console.log('submit login')
        } else {
          alert('校验失败')
        }
      })
    }
  }
}
</script>

<style scoped lang="less"></style>
