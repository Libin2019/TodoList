<template>
	<div class="hello">
		<top></top>
		<center></center>
	</div>
</template>

<script>

import Top from './top.vue'
import Center from './main.vue'
export default {
  name: 'HelloWorld',
  data () {
    return {
			
    }
  },
	components:{
		Top,
		Center,
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.hello{
		color: black;
	/* 	background: url(../assets/th.jpg); */
		background-size: 1920px 1080px;
		position: relative;
	}
	.hello:after{
		position: absolute;
		filter: blur(2px);
		-webkit-filter: blur(2px);
		z-index: 2;
	}
</style>
