<template>
  <div id="app">
    <h3>検索条件</h3>
    <div>
      <label>User Name</label>
      <!-- 変数 userName をバインディング -->
      <input v-model="userName" type="text" />
      <button v-on:click="search()">Search</button>
    </div>
    <h3>検索結果</h3>
    <table border="1">
      <thead>
        <tr>
          <!-- v-for で header をループ表示 -->
          <td v-for="item in header" :key="item">{{item}}</td>
        </tr>
      </thead>
      <tbody>
        <!-- v-for で userData をループ表示 -->
        <tr v-for="user in searchedUserData" :key="user.id">
          <td>
            <router-link :to="`/detail/${user.id}`">
              <a>{{user.id}}</a>
            </router-link>
          </td>
          <td>{{user.name}}</td>
        </tr>
      </tbody>
      <!-- 以下コメントアウトは、ユーザー情報を直書きした変数 userData を表示する場合 -->
      <!--
      <tr v-for="user in userData" :key="user.id">
        <td>
          <router-link :to="`/detail/${user.id}`">
            <a>{{user.id}}</a>
          </router-link>
        </td>
        <td>{{user.name}}</td>
      </tr>
      </tbody>
      -->
    </table>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import axios from "axios";

@Component
export default class Home extends Vue {
  userName: string = "";
  header: string[] = ["User Id", "User Name"];
  // ユーザー情報を直書きした変数
  userData = [
    { id: "001", name: "Tanaka" },
    { id: "002", name: "Tamura" },
    { id: "003", name: "Nakata" }
  ];
  // 検索結果で取得したユーザーを格納する変数
  searchedUserData = [];

  async search() {
    const response = await axios.get("http://localhost:3000/users", {
      params: {
        name_like: this.userName
      }
    });
    this.searchedUserData = response.data;
  }
}
</script>
