<template>
  <div class="container">
    <div class="login-container">
      <div class="login-right">
        <Login v-if="!showReset" @toResetPwd="handleResetPwd"></Login>
        <ForgetPassword v-else :show-reset="showReset" @toLogin="handleToLogin"></ForgetPassword>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue'
import viteLogo from '@/assets/logo-vite.svg'
import vueLogo from '@/assets/logo.png'
import Login from './components/loginForm.vue'
import ForgetPassword from './components/forgetPassword.vue'

export default defineComponent({
  name: 'Index',
  components: {
    Login,
    ForgetPassword
  },
  setup() {
    const showReset = ref(false)
    const handleResetPwd = () => {
      // 展示重置密码框
      showReset.value = true
    }
    const handleToLogin = () => {
      // 展示登录框框
      showReset.value = false
    }
    return {
      showReset,
      handleResetPwd,
      handleToLogin,
      vueLogo,
      viteLogo
    }
  }
})
</script>

<style lang="stylus" scoped>
.container{
    position: relative;
    background: url(../../assets/images/bg_login.png) no-repeat;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    .login-container{
        width:600px;
        min-width: 600px;
        height: 35%;
        min-height: 300px;
        flex-direction: row;
        display: flex;
        justify-content: space-evenly;
        border-radius: 10px;
        overflow: hidden;
        background-color :white;
        box-shadow:0 0 20px 5px rgba(34,84,142,.26);

        .login-right{
          width:100%;
          display:flex;
          flex-direction:column ;
          justify-content: center;
          align-items :center;
          padding:30px;

      }
    }

}
</style>
