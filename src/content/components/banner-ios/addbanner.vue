<template>
	<form class="form-horizontal" method="post">
	  	<fieldset>
		    <div class="control-group">
		      	<label class="control-label" for="focusedInput">七牛文件名</label>
		      	<div class="controls">
		        	<input class="input-xlarge focused" id="img" type="text" placeholder="七牛文件名(若有后缀包括后缀)" v-model="baniosimg" required>
		      	</div>
		    </div>
		    <div class="control-group">
		      	<label class="control-label" for="focusedInput">图片资源</label>
		      	<div class="controls">
		        	<input class="input-xlarge focused" id="url" type="text" placeholder="url" v-model="baniosurl" required>
		      	</div>
		    </div>
		    <div class="control-group">
		      	<label class="control-label" for="focusedInput">序号</label>
		      	<div class="controls">
		        	<input class="input-xlarge focused" id="num" type="text" placeholder="序号" v-model="baniosnum" required>
		      	</div>
		    </div>
	    </div>
	    <div class="form-actions">
	      <button class="btn btn-success" @click="addbanner">Add New <i class="icon-plus icon-white"></i></button>
	      <button type="reset" class="btn">Cancel</button>
	    </div>
	  </fieldset>
	</form>
</template>
<script>
var request = require('superagent');
export default {
	data(){
		return {
			baniosimg:"",
			baniosurl:"",
			baniosnum:""
		}
	},
	props: {
    	url: {
          	type: String
      	}
  	},
	methods:{
		addbanner: function(e){
			e.preventDefault()
			var self =  this
			if (this.baniosimg && this.baniosurl) {
				request
					.post(self.url + '/ios/banner/')
					.set('Authorization',localStorage.str)
					.send({img:self.baniosimg,url:self.baniosurl,num:self.baniosnum})
					.set('Content-Type','application/json')
					.end(function(err,res){
						if (err) throw err;
						if (res.status == 201) {
							alert('上传成功');
						}
						self.baniosimg = ''
						self.baniosurl = ''
						self.baniosnum = ''
					})
				}
		}
	}
}
</script>