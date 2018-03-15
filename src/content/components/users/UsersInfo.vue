<template>
    <div class="box">
      <div>
        <input class="input-xlarge focused" type="text" placeholder="学号" v-model.trim="stu_id" required>
      </div>
      <div>
        <input class="input-xlarge focused" type="text" placeholder="邮箱" v-model.trim="email" required>
      </div>
      <div>
        <input class="input-xlarge focused" type="password" placeholder="密码" v-model.trim="password" required>
      </div>
      <button class="btn btn-success" v-on:click="getInfo">获取信息</button>
      <div class="card border-success mb-3" style="max-width: 18rem;">
        <div class="card-body text-success">
          <p class="card-text">{{info}}</p>
        </div>
      </div>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        stu_id: "",
        email: "",
        password: "",
        info: "",
        isInfo: false
      }
    },
    methods: {
      getInfo() {
        fetch('https://ccnubox.muxixyz.com/api/cache/fetchinfo/', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Basic '+ btoa(this.email + ":" + this.password)
          },
          body: JSON.stringify({
            sid : parseInt(this.stu_id)
          })
        }).then(response => {
          if (response.ok) {
            return response.json()
            this.isInfo = true
          }
        }).then(value => {
          this.info = value
        })

      }
    }
  }
</script>
<style>
.box {
  margin-top: 50px;
}
</style>
