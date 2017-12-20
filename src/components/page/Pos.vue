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
								<el-button type="text" size="small" @click="deleteSingleGoods(scope.row)" >删除</el-button>
								
								<el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
							</template>
						</el-table-column>
					</el-table>
					<div class="divtotal">
						<a>总数{{totalCount}}</a>
						<a>总价{{totalMoney}}</a>
					</div>
					<div class="divbtn">
						<el-button type="warning">挂单</el-button>
						<el-button type="danger" @click="deleteOrderList()">删除</el-button>
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
					<li v-for="goods in oftenGoods"  @click="addOrderList(goods)"	> 
						<span>{{goods.goodsName}}</span>
						<span class="moneyColor">${{goods.price}}</span>
					</li>
					
				</ul>
			</div>
			
		</div>
		
		<el-tabs class="pos-tab" style="float:left;">
			<el-tab-pane  label="汉堡">
				<ul class="cooklist">
					<li v-for="goods in type0Goods" @click="addOrderList(goods)">
						<span><img :src="goods.goodsImg" width="100%"></span>
						<span>{{goods.goodsName}}</span>
						<span>{{goods.price}}元</span>
					</li>
				</ul>
			</el-tab-pane>
			<el-tab-pane  label="小食">
				<ul class="cooklist">
					<li v-for="goods in type1Goods"  @click="addOrderList(goods)">
						<span><img :src="goods.goodsImg" width="100%"></span>
						<span>{{goods.goodsName}}</span>
						<span>{{goods.price}}元</span>
					</li>
				</ul>
			</el-tab-pane>
			<el-tab-pane label="饮料">
				<ul class="cooklist">
					<li v-for="goods in type2Goods"  @click="addOrderList(goods)">
						<span><img :src="goods.goodsImg" width="100%"></span>
						<span>{{goods.goodsName}}</span>
						<span>{{goods.price}}元</span>
					</li>
				</ul>
			</el-tab-pane>
			<el-tab-pane label="套餐">
				<ul class="cooklist">
					<li v-for="goods in type3Goods"  @click="addOrderList(goods)">
						<span><img :src="goods.goodsImg" width="100%"></span>
						<span>{{goods.goodsName}}</span>
						<span>{{goods.price}}元</span>
					</li>
				</ul>
			</el-tab-pane>
		</el-tabs>
			
		</el-col>
		
	</el-row>
  </div>
</template>

<script  type="text/javascript">
import axios from 'axios'
export default {
  name: 'pos',
  data(){
	return{
		tableData:[],
		oftenGoods:[],
    type0Goods:[
          {
              goodsId:1,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'香辣鸡腿堡',
              price:18
          }
          
      ],
	totalCount:0,
	totalMoney:0,
	}
  },
  mounted:function()
  {
	document.getElementById("order-list").style.height=document.body.clientHeight+"px";
  },
  created:function()
  {      
		axios.get('http://jspang.com/DemoApi/oftenGoods.php')
      .then(response=>{
         console.log(response);
         this.oftenGoods=response.data;
      })
      .catch(error=>{
          console.log(error);
          alert('网络错误，不能访问');
      })
	  
	  
	        axios.get('http://jspang.com/DemoApi/typeGoods.php')
      .then(response=>{
         console.log(response);
         //this.oftenGoods=response.data;
         this.type0Goods=response.data[0];
         this.type1Goods=response.data[1];
         this.type2Goods=response.data[2];
         this.type3Goods=response.data[3];
		 
      })
      .catch(error=>{
          console.log(error);
          alert('网络错误，不能访问');
      })
  },
  methods:
  {
  
  	  getTotal()
	  {
		this.totalCount=0;
		this.totalMoney=0;
		
		if (this.tableData) {
                this.tableData.forEach((element) => {
                    this.totalCount += element.count;
                    this.totalMoney = this.totalMoney + (element.price * element.count);
                });
            }
	  },
	//添加订单列表的方法
      addOrderList(goods){
      
            let isHave=false;
            //判断是否这个商品已经存在于订单列表
            for (let i=0; i<this.tableData.length;i++){
                console.log(this.tableData[i].goodsId);
                if(this.tableData[i].goodsId==goods.goodsId){
                    isHave=true; //存在
                }
            }
            //根据isHave的值判断订单列表中是否已经有此商品
            if(isHave)
			{
                //存在就进行数量添加
                 let arr = this.tableData.filter(o =>o.goodsId == goods.goodsId);
                 arr[0].count++;
                 //console.log(arr);
            }
			else
			{
                //不存在就推入数组
                let newGoods={goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
                 this.tableData.push(newGoods);
 
            }
 
            //进行数量和价格的汇总计算
            this.getTotal();
			
           
      },
	  deleteOrderList()
	  {
		this.totalCount=0;
		this.totalMoney=0;
		this.tableData=[];
	  },
	  deleteSingleGoods(goods)
	  {
		//如果count=1,则直接删除
		if(goods.count==1)
		{
			this.tableData=this.tableData.filter(o=>o.goodsId!=goods.goodsId);
			
		}
		//如果count>1,则删除1个
		else
		{
			let arr=this.tableData.filter(o=>o.goodsId==goods.goodsId);
			arr[0].count--;
		}
		
		//计算总价和总量
		this.getTotal();
	  },


  }
  
}
/*
methods:{
	addOrderList(goods)
	{
	//商品是否已存在在订单列表中
		let isHave=false;
		for(let i=0;i<this.tableData.length;i++)
		{
			if(this.tableData[i].goodsId=goods.goodsId)
			{
				isHave=true;
			}
		}
	//根据判断的值编写业务逻辑
		if(isHave)
		{
			let array=this.tableData.filter(o=>o.goodsId.goodsId);
			arr[0].count++;
			
		}
		else
		{
			let newGoods={goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
            this.tableData.push(newGoods);
		}
	}

}
*/
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
	margin-left: 63px;
	margin-right:63px;
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
	width:18%;
	cursor:pointer;
}

.moneyColor
{
	Color:blue;
}
.cooklist li
{
	list-style: none;
	padding:10px;
	margin:5px;
	border:1px solid #E5E9F2;
	float:left;
	width:20%;
	border:1px solid #E5E9F2;
	cursor:pointer;
	
}
.pos-tab .el-tabs__content{
	overflow:auto;
	height:600px;
}
.divtotal a
{
	margin:20px;
	padding:20px;
}
</style>
