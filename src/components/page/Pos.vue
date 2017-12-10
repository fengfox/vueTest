<template>
  <div class="pos">
	<el-row>
		<el-col :span="7" class="pos-order" id="order-list">
			<el-tabs class="pos-tab">
				<el-tab-pane label="点餐">
					<el-table :data="tableData">
						<el-table-column prop="goodsName" label="商品名称">
							
						</el-table-column>
						<el-table-column prop="count" label="数量">
							
						</el-table-column>
						<el-table-column prop="price" label="金额">
							
						</el-table-column>
						<el-table-column  label="操作" fixed="right">
							<template scope="scope">
								<el-button type="text" size="small">删除</el-button>
								<el-button type="text" size="small">增加</el-button>
							</template>
						</el-table-column>
					</el-table>
					<div class="divbtn">
						<el-button type="warning">挂单</el-button>
						<el-button type="danger">删除</el-button>
						<el-button type="success">结账</el-button>
					</div>
				
				</el-tab-pane>
				<el-tab-pane label="挂单">挂单</el-tab-pane>
				<el-tab-pane label="外卖">外卖</el-tab-pane>
			</el-tabs>
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
  data(){
	return{
		tableData:[{
          
          goodsName: '可口可乐',
          price: 8,
          count:1
        }, {
          
          goodsName: '香辣鸡腿堡',
          price: 15,
          count:1
        }, {
         
          goodsName: '爱心薯条',
          price: 8,
          count:1
        }, {
         
          goodsName: '甜筒',
          price: 8,
          count:1
        }]
	}
  },
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
.pos-tab{
	margin:5%;
}
.divbtn{
	margin-top:10px;
}
</style>
