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
					<el-select v-model="inboundDate" filterable placeholder="入库日期">
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
            <el-form :inline="true">
                <el-form-item>
					<el-button type="success">物品入库</el-button>
                    <el-button type="warning" @click="outbound">物品出库</el-button>
                    <el-button class="btn">物品回收</el-button>
                    <el-button class="btn">物品删除</el-button>
                    <span>说明：物品入库是指将编码入库，物品出库是指将物品编码下拨给其他经销商</span>
				</el-form-item>
            </el-form>
            <div class="clear">
				<span class="el-icon-warning"></span>
				<p>已选择<span>{{selection.length}}</span>项</p>
				<a href="javascript:;" @click="clear">清空</a>
			</div>
		</el-col>

		<!--列表-->
		<el-table @sort-change="sort" :default-sort = "{prop: 'date', order: 'descending'}" class="table" border ref="multipleTable" :data="tableDate" highlight-current-row v-loading="listLoading" @selection-change="selsChange" style="width: 100%;">
			<el-table-column type="selection" width="55">
			</el-table-column>
			<!-- <el-table-column type="index" align="center" width="60" label="序号">
			</el-table-column> -->
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
			<el-table-column label="操作"  align="center">
				<template scope="scope">
					<el-button type="danger" size="small" @click="handleDel(scope.$index, scope.row)">删除</el-button>
				</template>
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
    name:'GoodsList',
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
        outbound(){
            //物品出库
            const h = this.$createElement;
            this.$msgbox({
                title: '您已选择('+this.selection.length+')条物品编码进行出库',
                center:'true',
                message: h('div', null, [
                    h('p', { style: 'color: black',}, '请选择经销商'),
                    h('p',{ style: 'margin: 20px 0' },[h('el-select', {attrs:{'placeholder':'所属省代'},on:{change:this.fn},props:{value:this.province}}, h('el-option',{props:{value:this.provincesAgent},domProps: {innerHTML: 'sssss'}},null)),]),
                    h('p',null,[h('el-select', {attrs:{placeholder:'所属网点'}}, null),]),
                    h('p',{ style: 'margin-top: 20px' },'说明:未选择网点,则直接出库给省代')
                ]),
                showCancelButton: true,
                confirmButtonText: '确认出库',
                cancelButtonText: '取消',
                beforeClose: (action, instance, done) => {
                    if (action === 'confirm') {
                    instance.confirmButtonLoading = true;
                    instance.confirmButtonText = '执行中...';
                    setTimeout(() => {
                        done();
                        setTimeout(() => {
                        instance.confirmButtonLoading = false;
                        }, 300);
                    }, 3000);
                    } else {
                    done();
                    }
                }
            }).then(action => {
                this.$message({
                    type: 'info',
                    message: 'action: ' + action
                });
            });
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
        clear(){
            //取消全部所选物品
            this.$refs.multipleTable.clearSelection(this.tableDate)
        },
        selsChange(selection){
            //选择物品
            this.selection=selection
        },
        handleDel(){
            //删除物品
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

