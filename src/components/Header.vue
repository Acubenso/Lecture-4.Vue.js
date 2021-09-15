<template>
  <header class="header">
    <a class="header-logo">
      <img src="../assets/logo.png" alt="Logo" />
      <h1>Рекуператори</h1>
      <p>Відчуй свіжість у своєму просторі</p>
    </a>
    <form class="header-search">
      <input
        class="header-search__input"
        type="text"
        placeholder="Пошук по сайту"
        aria-label="Пошук"
      />
      <button class="header-search__button" type="submit">Знайти</button>
    </form>
    <div class="header-options">
      <button class="header-options__button" type="button">Prana</button>
      <button class="header-options__button" type="button">Klimatronic</button>
      <button class="header-options__button" type="button">Blauberg</button>
      <button class="header-options__button" type="button">ME</button>
      <button class="header-options__button" type="button">Vents</button>
    </div>
    <div class="header-contacts">
      <h1>Контактні телефони:</h1>
      <p>(068)-68-68-688 (viber)</p>
      <p>(063)-63-63-633</p>
    </div>
    <div v-if="!isLogin" class="header-validation">
      <div class="header-validation-logIn">
        <router-link to="/login" class="black-text">
          <button class="header-validation-logIn_btn">
            Увійти
          </button>
        </router-link>
      </div>
      <div class="header-validation-register">
        <router-link to="/register" class="black-text">
          <button class="header-validation-register_btn">
            Зареєструватись
          </button>
        </router-link>
      </div>
    </div>
    <div v-else>
      <p class="nowrap">Привіт {{ name }}</p>
      <button
          v-on:click="unLogin"
          class="header-validation-logIn_btn">
        Вийти
      </button>
    </div>
    <button id="header-burger" class="header-burger">&#9776;</button>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: {},
  data: () => {
    return {
      isLogin: false,
      name: ''
    }
  },
  mounted() {
    const nameInfo = localStorage.getItem('login');
    if (nameInfo) this.name = nameInfo;

    const loginInfo = localStorage.getItem('isLogin');
    if (loginInfo) {
      this.isLogin = loginInfo === 'true';
    }
  },
  methods: {
    unLogin() {
      this.isLogin = false;
      localStorage.removeItem('login');
      localStorage.setItem('isLogin', this.isLogin);
    }
  }
};
</script>

<style scoped>
</style>
