<template>
  <div class="container">
    <div class="row">
      <div class="col-6">
        <h3>Категории "Приход"</h3>
        <div class="row">
          <div class="col-8">
            <input class="form-control" v-model="categoryPlus">
          </div>
          <button type="button" class="btn btn-success add" @click="addPlus()">
            <b>+ Добавить</b>
          </button>
        </div>

        <ul class="list-group" v-for="item of categoriesPlus" :key="item">
          <li class="list-group-item">
            <h6>{{item}}</h6>
          </li>
        </ul>
      </div>
      <div class="col-6">
        <h3>Категории "Расход"</h3>
        <div class="row">
          <div class="col-8">
            <input class="form-control" v-model="categoryMinus">
          </div>
          <button type="button" class="btn btn-success add" @click="addMinus()">
            <b>+ Добавить</b>
          </button>
        </div>
        <ul class="list-group" v-for="item of categoriesMinus" :key="item">
          <li class="list-group-item">
            <h6>{{item}}</h6>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Categories",
  props: ["categoriesPlus", "categoriesMinus"],
  data() {
    return {
      categoryPlus: "",
      categoryMinus: ""
    };
  },
  methods: {
      //Отправка на сервер категорий Приход
    addPlus() {
      var categoriesPlus = this.categoriesPlus;
      categoriesPlus.push(this.categoryPlus);
      this.$emit("categoriesPlus", categoriesPlus);
      axios
        .post(`http://localhost:8081/`, {
          body: categoriesPlus
        })
        .then(function(response) {
          console.log(response);
        })
        .catch(e => {
          this.errors.push(e);
        });
    },
    // Отправка на сервер категорий Расход
    addMinus() {
      var categoriesMinus = this.categoriesMinus;
      categoriesMinus.push(this.categoryMinus);
      this.$emit("categoriesMinus", categoriesMinus);
      axios
        .post(`http://localhost:8081/`, {
          body: categoriesMinus
        })
        .then(function(response) {
          console.log(response);
        })
        .catch(e => {
          this.errors.push(e);
        });
    }
  },
  components: {}
};
</script>

<style>
</style>
