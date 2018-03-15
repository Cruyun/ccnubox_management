<template>
    <div class="box">
      <div>
        <input class="input-xlarge focused" type="text" placeholder="学号" v-model.trim="stu_id" required>
      </div>
      <div>
        <input class="input-xlarge focused" type="password" placeholder="密码" v-model.trim="stu_passwd" required>
      </div>
      <button class="btn btn-success" v-on:click="getToken">获取 token</button>
      <div  class="card border-success mb-3" style="max-width: 18rem;">
        <div class="card-body text-success">
          <h5 class="card-title">Token</h5>
          <p class="card-text" v-if="this.isToken">{{token}}</p>
        </div>
      </div>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        stu_id: "",
        stu_passwd: "",
        token: "",
        isToken: false
      }
    },
    methods: {
      getToken() {
        //fetch('')
        this.token = "ector.js?type=script&index=0!./src/content/components/users/UsersInfo.vue 346 bytes "
        this.isToken = true
      }
    }
  }
</script>
<style>
.box {
  margin-top: 50px;
}
</style>