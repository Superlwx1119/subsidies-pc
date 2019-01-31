<template>
    <section>
        <!--工具条-->
		<el-col :span="24" class="toolbar" style="padding-bottom: 0px;">
			<el-form :inline="true" >
				<el-form-item>
					<el-select v-model="goodsState" filterable placeholder="物品状态">
                        <el-option
                        v-for="item in options"
                        :key="item"
                        :label="item"
                        :value="item">
                        </el-option>
                    </el-select>
				</el-form-item>
				<el-form-item>
					<el-select v-model="provincesAgent" filterable placeholder="所属省代">
                        <el-option
                        v-for="item in options"
                        :key="item"
                        :label="item"
                        :value="item">
                        </el-option>
                    </el-select>
				</el-form-item>
				<el-form-item>
					<el-select v-model="nodeAgent" filterable placeholder="所属网点">
                        <el-option
                        v-for="item in options"
                        :key="item"
                        :label="item"
                        :value="item">
                        </el-option>
                    </el-select>
				</el-form-item>
                <el-form-item>
					<el-input type="text" v-model="keyword" placeholder="请输入编码/型号关键字"></el-input>
				</el-form-item>
                <el-form-item>
					<el-button type="primary">查询</el-button>
                    <el-button type="primary">导出数据</el-button>
				</el-form-item>
			</el-form>
		</el-col>

		<!--列表-->
		<el-table @sort-change="sort" :default-sort = "{prop: 'date', order: 'descending'}" class="table" border ref="multipleTable" :data="tableDate" highlight-current-row v-loading="listLoading"  style="width: 100%;">
			<!-- <el-table-column type="selection" width="55">
			</el-table-column> -->
			<el-table-column type="index" align="center" width="60" label="序号">
			</el-table-column>
			<el-table-column prop="name" label="物品名称" align="center"  >
			</el-table-column>
			<el-table-column prop="model" label="物品型号"  align="center" >
			</el-table-column>
			<el-table-column prop="coding" label="物品编码"  align="center" >
			</el-table-column>
			<el-table-column prop="provinces" label="所属省代"  align="center" >
			</el-table-column>
			<el-table-column prop="branches" label="所属网点"  align="center">
			</el-table-column>
            <el-table-column prop="state" label="物品状态"  align="center">
			</el-table-column>
            <el-table-column prop="storageTime" label="入库时间"  align="center">
			</el-table-column>
            <el-table-column prop="cardNum" label="已办卡数量"  sortable align="center">
			</el-table-column>
            <el-table-column prop="succNum" label="已成功数量"  sortable align="center">
			</el-table-column>
		</el-table>

        <!--工具条-->
		<el-col :span="24" class="toolbar">
			<span>共150条数据 第1/80页</span>
			<el-pagination background :current-page="currentPage4" layout="prev, pager, next" @current-change="handleCurrentChange" :page-size="20" :total="total" style="float:right;">
			</el-pagination>
		</el-col>
    </section>
</template>

<script>
export default {
    name:'GoodsDetailRecycling',
    data(){
        return{
            currentPage4:1,
            selection:[],
            listLoading:false,
            total:0,
            goodsState:'',
            provincesAgent:'',
            nodeAgent:'',
            inboundDate:'',
            keyword:'',
            options:['1','2','3','4'],
            tableDate:[
                {
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },


                {
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },{
                    name:'aaaaaaaaaaaaa',
                    model:'bbbbbbbbbb',
                    coding:'ccccccccccc',
                    provinces:'dddddddddddddd',
                    branches:'eeeeeeeeeeeee',
                    state:'ffff',
                    storageTime:'ggggggggggggggggggggggg',
                    cardNum:'123',
                    succNum:'143'
                },
            ],
            sortField:'',
            sortWay:'',
            province:'',
            provincesAgent:['aaa','bbb','dddd','wwww']
        }
    },
    methods:{
        fn(){
            alert(222)
        },
        sort(column, prop, order){
            //排序
            this.sortField=column.prop
                if(column.order=='ascending'){
                    this.sortWay='asc'
                }else if(column.order=='descending'){
                    this.sortWay='desc' 
                }
            // this.search()
        },
        handleCurrentChange(){
            //选择当前页

        }
    }
}
</script>

<style lang="scss" scoped>
    section{
        background: white;
    }
    .toolbar{
        // width: 95%;
        margin: 0;
        background: white;
    }
    .table{
        margin: 10px;
    }
    .btn{
        background: #4ab9c3 !important;
        color: white;
    }
    .clear{
		display: flex;
		align-items: center;
		height: 30px;
		font-size: 14px;
		background: lightcyan;
		border: 1px solid lightskyblue;
		border-radius: 5px;
	}
	.clear p>span{
		color: lightskyblue;
	}
	.clear >span{
		margin: 0 5px;
		text-indent: 5px;
		font-weight: bold;
		color: cornflowerblue;
	}
	.clear a{
		display: inline-block;
		padding-left: 10px;
		text-decoration: none;
		color: lightskyblue;
	}
</style>


