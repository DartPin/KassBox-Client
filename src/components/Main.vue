<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-12">
          <button type="button" class="btn btn-primary add" @click="show = !show">
            <b>+ Добавить</b>
          </button>
        </div>
      </div>
    </div>
    <NewString
      v-if="show"
      :arrStrings="arrStrings"
      :categoriesPlus="categoriesPlus"
      :categoriesMinus="categoriesMinus"
      v-on:arrStrings="arrStrings = $event"
    ></NewString>

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
        <tr v-for="(item, i) of arrStrings.slice().reverse()" :key="item.id">
          <th scope="row">{{i+1}}</th>
          <td>{{item.nameDeal}}</td>
          <td>{{item.summ}}</td>
          <td>{{item.nameWhoGive}}</td>
          <td>{{item.nameWhoTake}}</td>
          <td>{{date = new Date(item.date).toLocaleString("ru", options)}}</td>
          <td>{{item.comment}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import NewString from "./NewString.vue";

export default {
  name: "Main",
  props: ["arrStrings", "categoriesPlus", "categoriesMinus"],
  data() {
    return {
      show: false,
      date: Date,
      options: {
        year: "numeric",
        month: "long",
        day: "numeric",
        timezone: "UTC",
        hour: "numeric",
        minute: "numeric"
      },
      i: 0
    };
  },
  computed: {},
  components: {
    NewString
  }
};
</script>

<style>
</style>
