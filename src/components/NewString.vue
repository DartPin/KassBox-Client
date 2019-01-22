<template>
  <div class="container box">
    <div class="row">
      <div class="col-2">
        <h5 class="inline">Выберите действие:</h5>
      </div>
      <div class="col">
        <select v-model="nameDeal" class="form-control dropdown-toggle">
          <option>Приход</option>
          <option>Расход</option>
        </select>
      </div>
    </div>
    <div class="row" v-if='nameDeal === "Приход"'>
      <div class="col-2">
        <h5 class="inline">Выберите категорию:</h5>
      </div>
      <div class="col">
        <select v-model="category" class="form-control dropdown-toggle">
          <option v-for="categ of categoriesPlus" :key="categ">{{categ}}</option>
        </select>
      </div>
    </div>
    <div class="row" v-else>
      <div class="col-2">
        <h5 class="inline">Выберите категорию:</h5>
      </div>
      <div class="col">
        <select v-model="category" class="form-control dropdown-toggle">
          <option v-for="categ of categoriesMinus" :key="categ">{{categ}}</option>
        </select>
      </div>
    </div>
    <div class="row">
      <div class="col-2">
        <h5>Кассир:</h5>
      </div>
      <div class="col">
        <input
          type="text"
          class="form-control"
          placeholder="Люльков Андрей"
          aria-label="Введите Фамилию и Имя: пример Люльков Андрей"
          v-model="nameWhoGive"
        >
      </div>
    </div>
    <div class="row">
      <div class="col-2">
        <h5>Выдано/Принято:</h5>
      </div>
      <div class="col">
        <input
          type="text"
          class="form-control"
          placeholder="Люльков Андрей/ ООО Апельсин"
          aria-label="Введите Фамилию и Имя: пример Люльков Андрей"
          v-model="nameWhoTake"
        >
      </div>
    </div>
    <div class="row">
      <div class="col-2">
        <h5>Введите сумму:</h5>
      </div>
      <div class="col">
        <input
          type="text"
          class="form-control"
          placeholder="0000.00"
          aria-label="Введите Фамилию и Имя: пример Люльков Андрей"
          v-model="summ"
        >
      </div>
    </div>
    <div class="row">
      <div class="col-2">
        <h5>Комментарий:</h5>
      </div>
      <div class="col">
        <input
          type="text"
          class="form-control"
          placeholder="подотчет"
          aria-label="Введите Фамилию и Имя: пример Люльков Андрей"
          v-model="comment"
        >
      </div>
    </div>
    <button type="button" class="btn btn-success add" @click="saveString(arrStrings)">
      <b>Сохранить</b>
    </button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "NewString",
  props: ["arrStrings", "categoriesPlus", "categoriesMinus"],
  data() {
    return {
      nameDeal: "",
      nameWhoGive: "",
      nameWhoTake: "",
      summ: "",
      comment: "",
      category: ""
    };
  },
  methods: {
    //Получение и отправка данных о новых приходах расходах на сервер
    saveString(value) {
      var newString = {};
      newString.nameDeal = this.nameDeal;
      newString.nameWhoGive = this.nameWhoGive;
      newString.nameWhoTake = this.nameWhoTake;
      newString.summ = Number(this.summ);
      newString.comment = this.comment;
      newString.date = new Date();
      newString.category = this.category;
      this.arrStrings.push(newString);
      this.$emit("arrStrings", this.value);
      axios
        .post(`http://localhost:8081/`, {
          body: newString
        })
        .then(function(response) {
          console.log(response);
        })
        .catch(e => {
          this.errors.push(e);
        });
    }
  }
};
</script>

<style>
</style>
