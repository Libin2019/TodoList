<template>
	<div class="todolist">
		<div class="form">
			<input type="text"  v-model.trim="value" @keyup.enter="add" placeholder="what you want to do ? ">
			<button class="btn" @click="add">Add</button>
		</div>
		<div class="amount clearfix">
			<h3 v-show="!items.length">当前没有任务&nbsp;&nbsp;&nbsp;</h3>
			<h3 v-show="items.length">当前所有任务数量：<span> {{ items.length }}&nbsp;&nbsp;&nbsp; </span></h3>
			<h3>当前已完成的数量：<span> {{ finished }} &nbsp;&nbsp;&nbsp;</span></h3>
			<h3>当前未完成的数量：<span>{{ unFinished }}&nbsp;&nbsp;&nbsp;</span></h3>
		</div>
		<div class="list">
			<ul>
				<li 
					v-for="(item,index) in items " 
					:key="index"
					:class="{ gray: item.finished  }"
					@mouseenter="enter(index)"
					@mouseleave="leave()">

					<input type="checkbox" v-model="item.finished" />
					<span>{{ item.message }}</span>
					<span  @click="del(index)" v-show="sel === index" name="del-icon">
						<img src="../assets/icon/delete.svg" alt="" width="30px" height="30px">
					</span>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
	export default {
		name:'center',
		data() {
			return {
				value:"",
				items:[
				],
				sel:-1,
			};
		},
		mounted(){
			
		},
		computed:{
			finished:function(){
				return this.items.filter(function(e){
					return e.finished
				}).length
			},
			unFinished:function(){
				return this.items.length - this.finished
			}
		},
		methods:{
			add(){
				let reg = /\s/g
				if(this.value !== ""){
					if(!reg.test(this.value)){
						this.items.unshift({ message:this.value , finished:false })
					}else{
						alert("不要含有空白字符")
					}
				}else{
					alert("不要含有空白字符")
				}
				this.value = ""
			},
			
			del(index){
				this.items.splice(index,1)
			},
			enter(index){
				this.sel = index
			},
			leave(){
				this.sel = -1
			}
		}
	}
</script>

<style scoped>
	.form input{
		height: 50px;
		width: 500px;
		text-indent: 10px;
		font-size: 25px;
		vertical-align: bottom;
		margin-left:30%;
	}
	.btn{
		color: white;
		background-color: #3a8ee6;
		height: 56px;
		width: 100px;
		border-width: 0px;
		/* border-radius: 3px; */
		cursor: pointer;
		outline: none;
		vertical-align: bottom;
		margin-left: -5px;
		font-size: 18px;
	}
	.btn:hover{
		background-color: #66b0ff;
	}
	.gray{
		color: gray;
		text-decoration: line-through;
	}
	.list ul{
		padding: 0;
	}
	.list ul li{
		list-style: none;
		text-align: left;
		width: 550px;
/* 		margin: 0 auto; */
		position: relative;
		font-size: 25px;
		margin-top: 10px;
/* 		border: 1px solid red; */
	}

	.list ul li span img{
		position: absolute;
		top: 1px;
		right: 50px;
		cursor: pointer;
	}
	.amount,.list{
		width: 50%;
		position: relative;
		left: 30%;
		
	}
	.amount h3{
		float: left;
	}
	.amount h3 span{
		color: red;
	}
	.clearfix:after{
		content:'';
		display:block;
		clear: both;
	}
	input[type="checkbox"]{
		-webkit-appearance: none;
		vertical-align:middle;
		background:#fff;
		border:#999 solid 1px;
		border-radius: 3px;
		min-height: 12px;
		min-width: 12px;
		width: 20px;
		height: 20px;
}
	input[type="checkbox"]:checked {
		background: #3190e8;
}
	input[type=checkbox]:checked::after{
		content: '';
		top: 13px;
		left: 9px;
		position: absolute;
		background: transparent;
		border: #fff solid 2px;
		border-top: none;
		border-right: none;
		height: 6px;
		width: 10px;
		-moz-transform: rotate(-45deg);
		-ms-transform: rotate(-45deg);
		-webkit-transform: rotate(-45deg); 
		transform: rotate(-45deg);
	}
</style>
