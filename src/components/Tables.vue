<template>
  <div class="container box">
    <div class="row">
      <div class="col-3">
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
      <div class="col-3">
        <h5 class="inline">Выберите категорию:</h5>
      </div>
      <div class="col">
        <select v-model="category" class="form-control dropdown-toggle">
          <option v-for="categ of categoriesPlus" :key="categ">{{categ}}</option>
        </select>
      </div>
    </div>
    <div class="row" v-else>
      <div class="col-3">
        <h5 class="inline">Выберите категорию:</h5>
      </div>
      <div class="col">
        <select v-model="category" class="form-control dropdown-toggle">
          <option v-for="categ of categoriesMinus" :key="categ">{{categ}}</option>
        </select>
      </div>
    </div>

    <table class="table table-striped">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">наименование</th>
          <th scope="col">сумма</th>
          <th scope="col">Кассир</th>
          <th scope="col">Кому/От кого было выдано/принято</th>
          <th scope="col">дата</th>
          <th scope="col">коментарий</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(item, i) of arrStrings.slice().reverse()"
          :key="item.id"
        >
          <th scope="row" v-if='category === item.category'>{{i+1}}</th>
          <td v-if='category === item.category'>{{item.nameDeal}}</td>
          <td v-if='category === item.category'>{{item.summ}}</td>
          <td v-if='category === item.category'>{{item.nameWhoGive}}</td>
          <td v-if='category === item.category'>{{item.nameWhoTake}}</td>
          <td v-if='category === item.category'>{{item.date.toLocaleString("ru", options)}}</td>
          <td v-if='category === item.category'>{{item.comment}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import NewString from "./NewString.vue";

export default {
  name: "Tables",
  props: ["arrStrings", "categoriesPlus", "categoriesMinus"],
  data() {
    return {
      nameDeal: "",
      category: ""
    };
  },
  methods: {
  },
  components: {}
};
</script>

<style>
</style>
