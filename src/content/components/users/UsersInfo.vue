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
      <div  class="card border-success mb-3" style="max-width: 18rem;">
        <div class="card-body text-success">
          <p class="card-text" v-if="isInfo">{{info}}</p>
        </div>
      </div>
    </div>
</template>

<script>
// var request = require('superagent');
  export default {
    data() {
      return {
        stu_id: {
          type: Number
        },
        email: "",
        password: "",
        token: "",
        isToken: false
      }
    },
    methods: {
      getInfo() {
        /*
        var self = this
        request
        .post('https://ccnubox.muxixyz.com/api/cache/fetchinfo/')
        .set('Content-Type', 'application/json')
        .set('Authorization','Basic '+ btoa(self.email + ":" + self.password))
        .send({"sid" : self.stu_id})
				.end(function(err,res){
          console.log("hah")
					if (err) throw err
					if (res.status == 200) {
							self.info = json
              self.isInfo = true
						}
        })
        */
        fetch('https://ccnubox.muxixyz.com/api/cache/fetchinfo/', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Basic '+ btoa(this.email + ":" + this.password)
          },
          body: {
            "sid" : this.stu_id
          }
        }).then(response => {
          if (response.ok)
            response.json()
        }).then(json => {
          this.info = json
          this.isInfo = true
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
