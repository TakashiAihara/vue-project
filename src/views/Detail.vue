<template>
  <div id="app">
    <dl>
      <dt>User Id</dt>
      <dd>{{userId}}</dd>
      <dt>User Name</dt>
      <dd>{{userName}}</dd>
    </dl>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import axios from "axios";

@Component
export default class UserDetail extends Vue {
  userId: string = "";
  userName: string = "";

  // インスタンスライフサイクルフックによる割り込み処理
  async created() {
    this.userId = this.$route.params.id;
    const response = await axios.get("http://localhost:3000/users", {
      params: {
        id: this.userId
      }
    });
    this.userName = response.data[0].name;
  }
}
</script>