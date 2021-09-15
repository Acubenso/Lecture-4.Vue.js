<template>
  <div class="page__body">
    <div class="form">
      <form @submit.prevent="submitHandler" class="form__body" id="form">
        <h1 class="form-title">Вхід</h1>
        <div class="form-item">
          <label for="formName" class="form__label">Логін*</label><br />
          <input 
            autocomplete="off" 
            id="formName" 
            type="text" 
            name="name" 
            class="form__input 
            w-100" 
            v-model="login"
            :class="{invalid: $v.login.$dirty && !$v.login.required || $v.login.$dirty && !$v.login.minLength}" 
          />
          <small
              v-if="$v.login.$dirty && !$v.login.required"
              class="helper-text invalid">Введіть коректний логін
          </small>
          <small
              v-else-if="$v.login.$dirty && !$v.login.minLength"
              class="helper-text invalid">Логін повинен мати {{ $v.login.$params.minLength.min }} і більше символів.<br/>Зараз є - {{ login.length }}
          </small>
        </div>
        <div class="form-item">
          <label for="formPassword" class="form__label">Пароль*</label><br />
          <input
            autocomplete="off"
            id="formPassword"
            type="text"
            name="password"
            class="form__input w-100"
            v-model="password"
            :class="{invalid: $v.password.$dirty && !$v.password.required || $v.password.$dirty && !$v.password.minLength}"
          />
          <small
              v-if="$v.password.$dirty && !$v.password.required"
              class="helper-text invalid">Введіть коректний пароль</small>
          <small
              v-else-if="$v.password.$dirty && !$v.password.minLength"
              class="helper-text invalid">Пароль повинен мати {{ $v.password.$params.minLength.min }} і більше символів.<br/>Зараз є - {{ password.length }}</small>
        </div>
        <div class="beetween">
          <button type="submit" class="btn">Увійти</button>
          <router-link to="/" class="black-text">
            <button class="back">
              Назад
            </button>
          </router-link>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { required, minLength } from 'vuelidate/lib/validators';

export default {
  name: "Login",
  props: {},
  data: () => {
    return {
      login: '',
      password: ''
    }
  },
  validations: {
    login: { required, minLength: minLength(4) },
    password: { required, minLength: minLength(6) }
  },
  methods: {
    submitHandler() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }

      localStorage.setItem('login', this.login);
      localStorage.setItem('isLogin', true);

      this.$router.push("/");
    }
  }
};
</script>

<style scoped>
input.invalid {
  border: 1px solid red;
}

small.invalid {
  padding-top: 5px;
  color: red;
}

.w-100 {
  width: 97%;
}

.beetween {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 0.8em;
}
.page__body {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #eaf3f0;
  min-height: 100vh;
}
.form {
  min-width: 22em;
  min-height: 15em;
  background-color: #cdd1d0;
  border: 1px solid black;
  border-radius: 1em;
}
.form-title {
  margin: 0.5em 0 0 0;
}
.form__body {
  width: 60%;
  margin: 0 auto;
}
.form-item {
  margin-top: 0.5em;
}
.form-input {
  width: 100%;
}
.btn {
  background-color: #22e0dd;
  padding: 0.3em;
  cursor: pointer;
  border-radius: 0.5em;
}
.btn:hover {
  background-color: #1ffffb;
}
</style>
