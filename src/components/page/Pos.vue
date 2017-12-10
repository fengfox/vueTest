<template>
  <div class="pos">
	<el-row>
		<el-col :span="7" class="pos-order" id="order-list">
			我是订单
		</el-col>
		<el-col>
		    我是产品
		</el-col>
	</el-row>
  </div>
</template>

<script  type="text/javascript">
export default {
  name: 'pos',
  mounted:function()
  {
	document.getElementById("order-list").style.height=document.body.clientHeight+"px";
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
.pos-order{
	background-color:#F9FAFC;
	border-right:1solid #C0CCDA;
}
</style>
