<template>
<form class="form-horizontal">
  	<fieldset>
	    <div class="control-group">
	      	<label class="control-label" for="focusedInput">version</label>
	      	<div class="controls">
	        	<input class="input-xlarge focused" id="focusedInput" v-model="ptcver" type="text" placeholder="v">
	      	</div>
	    </div>
	    <div class="control-group">
	      	<label class="control-label" for="focusedInput">下载地址</label>
	      	<div class="controls">
	        	<input class="input-xlarge focused" id="focusedInput" v-model="ptcdnl" type="text" placeholder="url">
	      	</div>
	    </div>
	    <div class="control-group">
	      	<label class="control-label" for="focusedInput">更新时间</label>
	      	<div class="controls">
	        	<input class="input-xlarge focused" id="focusedInput" v-model="ptcupdt" type="text" placeholder="2016-0802">
	      	</div>
	    </div>
	    <div class="control-group">
	      	<label class="control-label" for="focusedInput">更新说明</label>
	      	<div class="controls">
	        	<input class="input-xlarge focused" id="focusedInput" v-model="ptcintro" type="text" placeholder="更新了...">
	      	</div>
	    </div>
	    <div class="control-group">
	      	<label class="control-label" for="focusedInput">补丁包大小</label>
	      	<div class="controls">
	        	<input class="input-xlarge focused" id="focusedInput" v-model="ptcsize" type="text" placeholder="M">
	      	</div>
	    </div>
    </div>
    <div class="form-actions">
      <button class="btn btn-success" @click="addpatch">Add New <i class="icon-plus icon-white"></i></button>
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
			ptcver:'',
			ptcdnl:'',
			ptcupdt:'',
			ptcintro:'',
			ptcsize:''
		}
	},
	props: {
    	url: {
          	type: String
      	}
  	},
	methods:{
		addpatch: function(e){
			e.preventDefault()
			var self =  this
			request
				.post(self.url + '/patch/')
				.set('Authorization',localStorage.str)
				.send({version:self.ptcver,download:self.ptcdnl,update:self.ptcupdt,intro:self.ptcintro,size:self.ptcsize})
				.end(function(err,res){
					if (err) throw err;
					if (res.status == 201) {
						alert(res.body.msg);
					}
					self.ptcver =''
					self.ptcdnl=''
					self.ptcupdt=''
					self.ptcintro=''
					self.ptcsize=''
				})
		}
	}
}
</script>