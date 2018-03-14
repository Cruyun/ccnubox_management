<template>
	<div>
		<div>
			<h1>用户信息</h1>
		</div>
			<router-view :url="url"></router-view>
		</div>
</template>

<script>
	export default {
		props: {
			url: {
				type: String
			}
		}
	}
</script>