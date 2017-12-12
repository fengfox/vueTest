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
		<el-col :span='17' class="pos-order" id="order-list">
		<div class="goods">
			<div class="title"><a style="float:left;">常用商品</a></div>
			
			<div class="goodlist">
				<ul>
					<li v-for="goods in oftenGoods"> 
						<span>{{goods.goodsName}}</span>
						<span class="moneyColor">${{goods.price}}</span>
					</li>
					
				</ul>
			</div>
			
		</div>
		
		<el-tabs class="pos-tab" style="float:left;">
			<el-tab-pane  label="汉堡">
				汉堡
			</el-tab-pane>
			<el-tab-pane  label="小食">
				小食
			</el-tab-pane>
			<el-tab-pane label="饮料">
				饮料
			</el-tab-pane>
			<el-tab-pane label="套餐">
				套餐
			</el-tab-pane>
		</el-tabs>
			
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
        }],
		oftenGoods:[
          {
              goodsId:1,
              goodsName:'香辣鸡腿堡',
              price:18
          }, {
              goodsId:2,
              goodsName:'田园鸡腿堡',
              price:15
          }, {
              goodsId:3,
              goodsName:'和风汉堡',
              price:15
          }, {
              goodsId:4,
              goodsName:'快乐全家桶',
              price:80
          }, {
              goodsId:5,
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
              goodsName:'魔法鸡块',
              price:20
          }, {
              goodsId:7,
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
              goodsName:'雪顶咖啡',
              price:18
          }, {
              goodsId:9,
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:20,
              goodsName:'香脆鸡柳',
              price:17
          }
          
      ]
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
.goods{
	margin:20px;
	float:left;
}
.title{
	
       height: 20px;
       border-bottom:1px solid #D3DCE6;
       background-color: #F9FAFC;
       padding:10px;
   }
.goodlist ul li{
	list-style: none;
	padding:10px;
	margin:5px;
	border:1px solid #E5E9F2;
	float:left;

}
li{
	width:15%;
}
.moneyColor
{
	Color:blue;
}
</style>
