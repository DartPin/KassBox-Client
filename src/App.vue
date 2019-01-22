<template>
  <div id="app">
    <Header
      :MorningSumm="MorningSumm"
      :totalSumm="totalSumm"
      :componentName="componentName"
      @newName="componentName = $event"
    ></Header>
    <component
      :arrStrings="arrStrings"
      v-on:arrStrings="arrStrings = $event"
      :categoriesPlus="categoriesPlus"
      v-on:categoriesPlus="categoriesPlus = $event"
      :categoriesMinus="categoriesMinus"
      v-on:categoriesMinus="categoriesMinus = $event"
      v-bind:is="currentNameComponent"
    ></component>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import Tables from "./components/Tables.vue";
import Categories from "./components/Categories.vue";
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
      data: "",
      arrStrings: [],
      componentName: "Main",
      total: 0,
      categoriesPlus: "",
      categoriesMinus: []
    };
  },
  created() {
    //получение данных с сервера и их разбивка на категории и базу движения ДС
    axios.get("http://localhost:8081/").then(response => {
      this.data = response.data;
      this.arrStrings = this.data[0].arrStrings;
      this.categoriesPlus = this.data[0].categoriesPlus;
      this.categoriesMinus = this.data[0].categoriesMinus;
    });
  },
  computed: {
    //Расчет суммы итоговой
    totalSumm: function() {
      this.total = 0;
      this.arrStrings.forEach(item => {
        if (item.nameDeal === "Приход") {
          this.total += item.summ;
        } else {
          this.total -= item.summ;
        }
      });
      return this.total;
    },
    //Расчет суммы в кассе на утро(00:00 часов)
    MorningSumm: function() {
      var MorningDate = new Date();
      MorningDate.setHours(0, 0, 0, 0);
      var total = 0;
      this.arrStrings.forEach(item => {
        var d = new Date(item.date);
        if (d < MorningDate) {
          if (item.nameDeal === "Приход") {
            total += item.summ;
          } else {
            total -= item.summ;
          }
        }
      });
      return total;
    },
    //получение имя компонента отражающегося в основной части экрана
    currentNameComponent: function() {
      return this.componentName;
    }
  },
  components: {
    Header,
    Main,
    Tables,
    Categories
  }
};
</script>

<style>
</style>
