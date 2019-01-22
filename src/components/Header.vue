<template>
  <header>
    <nav class="navbar navbar-expand-lg navbar-light menu">
      <a class="navbar-brand" href="#">
        <img src="/src/assets/logo.gif" width="120" height="120">
      </a>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active-link">
            <a class="nav-link" href="#" @click="newComponentName('Main')">главная</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#" @click="newComponentName('Tables')">отчеты</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#" @click="newComponentName('Categories')">категории</a>
          </li>
        </ul>
      </div>
      <div>
        <h2>Сейчас в кассе: {{totalSumm}} руб.</h2>
        <h6>Сумма на утро: {{MorningSumm}} руб.</h6>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: ["totalSumm", "componentName", "MorningSumm"],
  data() {
    return {};
  },
  methods: {
    //обработка имени компонента главной части экрана при нажатии 
    newComponentName: function(value) {
      this.$emit("newName", value);
    }
  }
};
</script>

<style>
</style>
