<template>
  <div class="login-register-page">
    <div class="login-bg">
     <login-bg/>
    </div>
    <form
      action="javascript:void(0);"
      class="login-form"
      :style="{ padding: padding }"
    >
      <h1>{{ formName }}</h1>
      <div class="form-control">
        <input
          type="text"
          name="username"
          v-model="formData.username"
          id="username"
          placeholder=" "
          autocomplete="off"
        />
        <label for="username">账号</label>
      </div>
      <div class="form-control">
        <input
          type="password"
          name="password"
          v-model="formData.password"
          id="password"
          placeholder=" "
          autocomplete="off"
        />
        <label for="password">密码</label>
      </div>
      <button type="submit" class="submit-btn" @click="submit">
        {{ submitName }}
      </button>
      <div class="change-type">{{ tips }}<span @click="changeType">{{ action }}</span></div>
    </form>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      userType: 0,
      padding: "50px 40px",
      formName: "注册",
      submitName: '提交',
      formData: {
        username: "",
        password: ""
      },
      tips: '没有账号,点击',
      action: '注册'
    };
  },
  methods: {
    submit() {},
    changeType() {}
  }
};
</script>
<style lang="scss" scoped>
.login-register-page {
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    .login-bg{
      position: absolute;
      width: 100vw;
      height: 100vh;
      overflow: hidden;
    }
  .login-form {
    width: 600px;
    display: flex;
    flex-direction: column;
    align-items: center;
    position: absolute;
    z-index: 10;
    color: white;
    background: rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    box-shadow: 0 0.4px 0.4px rgba(128, 128, 128, 0.109),
      0 1px 1px rgba(128, 128, 128, 0.155),
      0 2.1px 2.1px rgba(128, 128, 128, 0.195),
      0 4.4px 4.4px rgba(128, 128, 128, 0.241),
      0 12px 12px rgba(128, 128, 128, 0.35);

    h1 {
      margin: 0 0 24px 0;
      font-size: 36px;
    }

    .btn {
      width: 100%;
      margin: 18px 0 9px 0;
    }
    .form-control {
      --default-color: currentColor;
      --invalid-color: #e74c3c;
      --valid-color: #3498db;
      --border-bottom-color: currentColor;

      position: relative;
      border-bottom: 1px solid var(--border-bottom-color);
      margin: 18px 0;
      &::after {
        position: absolute;
        content: "";
        left: 0;
        bottom: -1px;
        width: 100%;
        height: 2px;
        background: var(--valid-color);
        transform: scaleX(0);
        transform-origin: left;
        transition: 0.3s;
      }

      &:focus-within::after {
        transform: scaleX(1);
      }
      input {
        padding: 8px 0;
        font-size: inherit;
        font-weight: inherit;
        color: currentColor;
        background: transparent;
        border: none;
        outline: none;
        &:invalid ~ label {
          color: var(--invalid-color);
        }

        &:valid ~ label {
          color: var(--valid-color);
        }

        &:placeholder-shown ~ label {
          color: var(--default-color);
        }
        &:focus ~ label {
          transform: translateY(-120%) scale(0.75);
        }
        &:not(:placeholder-shown) ~ label {
          transform: translateY(-120%) scale(0.75);
       }
      }

      label {
        position: absolute;
        top: 8px;
        left: 0;
        transition: 0.3s;
        transform-origin: left;
      }
    }
    .submit-btn {
      position: relative;
      width: 80%;
      padding: 6px 0;
      margin: 25px 0;
      font-size: 16px;
      color: currentColor;
      background: transparent;
      border: 2px solid hsla(204, 70%, 53%, 1);
      outline: none;
      cursor: pointer;
      overflow: hidden;
      transition: 0.6s;

      &::before {
        position: absolute;
        content: "";
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: linear-gradient(
          120deg,
          transparent,
          hsla(204, 70%, 53%, 0.5),
          transparent
        );
        transform: translateX(-100%);
        transition: 0.6s;
      }

      &:hover {
        box-shadow: 0 0 20px 10px hsla(204, 70%, 53%, 0.5);
      }

      &:hover::before {
        transform: translateX(100%);
      }
    }
    .change-type{
      letter-spacing: 2px;
      span {
        cursor: pointer;
        color: #007fff
      }
    }
  }
}

@media screen and (max-width: 700px) {
  .login-register-page {
    .login-form {
      width: 90%;
      padding: 26px 20px !important;
      h1 {
        margin: 0 0 24px 0;
        font-size: 24px;
      }
    }
    .form-control {
      width: 40vw;
      margin: 18px 0;
    }
    .code {
      width: 80px;
      right: -80px !important;
      top: -5px !important;
    }
  }
}
</style>
