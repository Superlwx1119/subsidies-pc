<template>
    <div>
        <div v-if="$store.state.show">
        <el-col :span="24" class="toolbar" style="padding-bottom: 0px;">
            <el-form :inline="true" class="form">
                <el-form-item>
                    <p>出库时间 :</p>
                </el-form-item>
                <el-form-item>
                    <el-input placeholder="出库时间" type="text" v-model="IncomingBatches"></el-input>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary">查询</el-button>
                </el-form-item>
            </el-form>
        </el-col>  
        <el-table @sort-change="sort" :default-sort = "{prop: 'date', order: 'descending'}" class="table" border ref="multipleTable" :data="tableDate" highlight-current-row v-loading="listLoading"  style="width: 100%;">
			<!-- <el-table-column type="selection" width="55">
			</el-table-column> -->
			<el-table-column type="index" align="center" width="60" label="序号">
			</el-table-column>
			<el-table-column prop="time" label="出库时间" align="center"  >
			</el-table-column>
			<el-table-column prop="dealers" label="所属经销商"  align="center" >
			</el-table-column>
            <el-table-column prop="number" label="出库数量"  sortable align="center">
			</el-table-column>
            <el-table-column prop="state" label="出库状态"  align="center">
			</el-table-column>
			<el-table-column label="操作"  align="center">
				<template scope="scope">
					<el-button  size="small" @click="showDetail(scope.$index, scope.row)">查看明细</el-button>
				</template>
			</el-table-column>
		</el-table>

        <!--分页-->
		<el-col :span="24" class="toolbar">
			<span>共150条数据 第1/80页</span>
			<el-pagination background layout="prev, pager, next" :current-page="currentPage4" @current-change="handleCurrentChange" :page-size="20" :total="total" style="float:right;">
			</el-pagination>
		</el-col>
        </div>
        <div v-if="!$store.state.show">
            <transition name="fade" mode="out-in">
                <router-view></router-view>
            </transition>
        </div>
    </div>
</template>

<script>
import Qs from 'qs'
import axios from 'axios'
import store from '@/store';
export default {
    name:'OutboundRecords',
    data(){
        return{
            IncomingBatches:'',
            sortField:'',
            sortWay:'',
            total:0,
            listLoading:false,
            currentPage4:1,
            tableDate:[{
                time:'2019-01-05',
                dealers:'忘光我欧尼瓯炯',
                number:'659',
                state:'1'
            }]
        }
    },
    methods:{
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
        },
        showDetail(){
            //查看明细
            this.$router.push('/GoodsDetailOut')
            store.dispatch('showDetail',true)
        }
    }
}
</script>

<style lang="scss" scoped>
    .toolbar{
        // width: 95%;
        margin: 0;
        background: white;
        .form{
            padding: 10px;
        }
    }
</style>

