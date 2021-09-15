<template>
  <div class="page__body">
    <div class="form">
      <form @submit.prevent="submitHandler" class="form__body" id="form">
        <h1 class="form-title">Реєстрація</h1>
        <div class="form-item">
          <label for="formName" class="form__label">Логін*</label><br />
          <input v-model="login" autocomplete="off" id="formName" type="text" name="name" class="form__input w-100"
                 :class="{invalid: $v.login.$dirty && !$v.login.required || $v.login.$dirty && !$v.login.minLength}"
          />
          <small
              v-if="$v.login.$dirty && !$v.login.required"
              class="helper-text invalid">Введіть свій логін</small>
          <small
              v-else-if="$v.login.$dirty && !$v.login.minLength"
              class="helper-text invalid">Логін повинен мати {{ $v.login.$params.minLength.min }} і більше символів.<br/>Зараз є - {{ login.length }}</small>

        </div>
        <div class="form-item">
          <label for="formPassword" class="form__label">Пароль*</label><br />
          <input
            v-model="password"
            autocomplete="off"
            id="formPassword"
            type="text"
            name="password"
            class="form__input w-100"
            :class="{invalid: $v.password.$dirty && !$v.password.required || $v.password.$dirty && !$v.password.minLength}"
          />
          <small
              v-if="$v.password.$dirty && !$v.password.required"
              class="helper-text invalid">Введіть свій пароль</small>
          <small
              v-else-if="$v.password.$dirty && !$v.password.minLength"
              class="helper-text invalid">Пароль повинен мати {{ $v.password.$params.minLength.min }} і більше символів.<br/>Зараз є - {{ password.length }}</small>
        </div>
        <div class="form-item">
          <label for="formEmail" class="form__label">E-mail*</label><br />
          <input
              :class="{invalid: $v.email.$dirty && !$v.email.required || $v.email.$dirty}"
              v-model="email" autocomplete="off"  id="formEmail" type="text" name="email" class="form__input w-100" />
          <small
              v-if="$v.email.$dirty && !$v.email.email"
              class="helper-text invalid">Введіть правильний e-mail</small>
          <small
              v-else-if="$v.email.$dirty && !$v.email.required"
              class="helper-text invalid">Введіть свій e-mail</small>
        </div>
        <div class="beetween">
          <button type="submit" class="btn">Зареєструватись</button>
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
import { email, required, minLength } from 'vuelidate/lib/validators';

export default {
  name: "Register",
  props: {},
  data: () => {
    return {
      login: '',
      email: '',
      password: ''
    }
  },
  validations: {
    email: { email, required },
    login: { required, minLength: minLength(4) },
    password: { required, minLength: minLength(6) }
  },
  methods: {
    submitHandler() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }

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
  min-height: 100vh;
  margin: 0;
  background-color: #eaf3f0;
}
.form {
  min-width: 22em;
  min-height: 20em;
  background-color: #cdd1d0;
  border: 1px solid black;
  border-radius: 1em;
}
.form-title {
  margin: 0.5em 0 0 0;
}
.form__body {
  position: relative;
  width: 60%;
  margin: 0 auto;
}
.form-item {
  margin-top: 0.5em;
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
