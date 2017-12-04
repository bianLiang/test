<template>
	<div id="chi1">
		<span @click='home_page()'>首页</span>
		<span @click='up()'>上一页</span>
		<ul>
			<li v-for='(item,index) in arr' @click='fn(index)' :class="{'addcolor':ind === index}" v-show='item.bol'>{{item.de}}</li>
		</ul>
		<span @click='down()'>下一页</span>
		<span @click='Shadowe()'>尾页</span>
		<span>当前第{{ current }}页，共有30页</span>
		<input type="text" name="" v-model='gos'>
		<span class="go" @click='go()'>Go</span>
	</div>
</template>
<style>
	*{margin: 0;padding: 0;list-style-type: none; }
	#chi1 span,#chi1 input,#chi1 ul{
		float: left;
	}
	#chi1{
		width: 900px;
		margin: 0 auto;
		zoom:1;
	}
	#chi1:after {
    content:""; 
    display:block;
    clear:both;
} 
	#chi1 ul li{
		float: left;
		padding: 5px;
		border: 1px solid #ccc;
	}
	#chi1 span{
		margin-right: 10px;
	}
	#chi1 span,#chi1 li{
		cursor: pointer;
	}
	.go{
	 	background: #ccc;
    	padding: 1px 7px;
	}


	.addcolor{
		color: #fff;
    	background:blue;
	}
</style>




<script>
  export default{
  	props:['mark'],
    data:function() {
      	return{
      		arr:[
      				{de:1,bol:true},
      				{de:2,bol:true},
      				{de:3,bol:true},
      				{de:4,bol:true},
      				{de:5,bol:true},
      				{de:6,bol:true},
      				{de:7,bol:true},
      				{de:8,bol:true},
      				{de:9,bol:true},
      				{de:10,bol:true},
      				{de:11,bol:false},
      				{de:12,bol:false},
      				{de:13,bol:false},
      				{de:14,bol:false},
      				{de:15,bol:false},
      				{de:16,bol:false},
      				{de:17,bol:false},
      				{de:18,bol:false},
      				{de:19,bol:false},
      				{de:20,bol:false},
      				{de:21,bol:false},
      				{de:22,bol:false},
      				{de:23,bol:false},
      				{de:24,bol:false},
      				{de:25,bol:false},
      				{de:26,bol:false},
      				{de:27,bol:false},
      				{de:28,bol:false},
      				{de:29,bol:false},
      				{de:30,bol:false}
      		],
      		ind: 0,
      		gos:'',
      		current:'1'
      		}
    },
    methods:{
    	//设置点击列表事件，使用this.$emit将数据传到父组件里的子组件中
		fn:function(index){
			this.ind = index;
			this.$emit('change',this.arr[index].de);
			this.current=this.ind+1;
		},
		//设置下一页点击事件
		down:function() {
			this.ind++;
			if(this.ind>29){
				this.ind=29;
			}
			this.current=this.ind+1;
			console.log(this.ind)
			if(this.ind%10==0){
				for(var i=0;i<this.arr.length;i++){
					this.arr[i].bol=false;
					for(var k=0;k<10;k++){
					this.arr[this.ind+k].bol=true;
					this.current=this.ind+1;
					
					}
				}	
			}
			this.$emit('change',this.arr[this.ind].de);
		},
		//设置上一页点击事件
		up:function() {
			this.ind--;
			if(this.ind<0){
				this.ind=0;
			}

			console.log(this.ind)
			if(this.ind%10==9){
				for(var i=0;i<this.arr.length;i++){
					this.arr[i].bol=false;
					
					for(var j=0;j<10;j++){
					this.arr[this.ind-j].bol=true;
					this.current=this.ind+1;
					}
				}	
			};
			this.$emit('change',this.arr[this.ind].de);
		},
		//设置首页点击事件
		home_page:function() {
			this.ind=0;
			for(var i=0;i<this.arr.length;i++){
				this.arr[i].bol=false;
				for(var k=0;k<10;k++){
					this.arr[this.ind+k].bol=true;
				}
			}
			this.current=this.ind+1;
			this.$emit('change',this.arr[this.ind].de);
		},
		//设置尾页点击事件
		Shadowe:function() {
			this.ind=29;
			for(var i=0;i<this.arr.length;i++){
					this.arr[i].bol=false;
					
					for(var j=0;j<10;j++){
					this.arr[this.ind-j].bol=true;
					}
				}
			this.current=this.ind;
			this.$emit('change',this.arr[this.ind].de);
		},
		//设置跳页事件
		go:function() {
			if(this.gos-1<29){
				this.gos=Math.abs(parseInt(this.gos));
				this.ind =this.gos-1;
				this.current=this.gos;


				for(var i=0;i<this.arr.length;i++){
					this.arr[i].bol=false;
					if(this.gos<10){
						for(var k=0;k<10;k++){
							this.arr[k].bol=true;
						}
					}else if(this.gos<20){
						for(var k=0;k<10;k++){
							this.arr[k+10].bol=true;
						}
					}else{
						for(var k=0;k<10;k++){
							this.arr[k+20].bol=true;
						}
					}
				};
				this.gos=''	;
			}else if(this.gos<0){
				this.gos=0;
				this.current=0;
				alert("请输入正确页数")
			}else if(this.gos>30){
				alert("请输入小于或等于30的数字")
			}
			
			this.$emit('change',this.arr[this.ind].de);
		}
    }
  }

</script>