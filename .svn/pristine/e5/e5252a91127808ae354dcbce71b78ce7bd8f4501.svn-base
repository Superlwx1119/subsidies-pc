<template>
    <div class="goods">
        <el-row    class="statistical">
            <el-col :span="4" class="model"> 
                <div>
                    <span class="title">物品总数: </span>
                    <span class="num"> 12560</span>
                </div>
            </el-col>
            <el-col :span="4" :offset="1" class="model">
                <div>
                    <span class="title">已注册总数: </span>
                    <span class="num"> 5000</span>
                </div>
            </el-col>
            <el-col :span="4" :offset="1" class="model">
                <div>
                    <span class="title">未注册总数: </span>
                    <span class="num"> 2560</span>
                </div>
            </el-col>
            <el-col :span="4" :offset="1" class="model">
                <div>
                    <span class="title">已出库数: </span>
                    <span class="num"> 8560</span>
                </div>
            </el-col>
            <el-col :span="4" :offset="1" class="model">
                <div>
                    <span class="title">未出库数:</span>
                    <span class="num">6560</span>
                </div>
            </el-col>
        </el-row>   
        <el-row class="table">
            <el-col :span="24">
                <el-select v-model="inboundDate" filterable placeholder="所属省代">
                    <el-option
                    v-for="item in options"
                    :key="item"
                    :label="item"
                    :value="item">
                    </el-option>
                </el-select>
                <el-select v-model="inboundDate" filterable placeholder="所属网点">
                    <el-option
                    v-for="item in options"
                    :key="item"
                    :label="item"
                    :value="item">
                    </el-option>
                </el-select>
            </el-col>
        </el-row>
    </div>
</template>

<script>
export default {
    name:'GoodsStatistics',
    data(){
        return{
            options:[1,2,3,4,5,6],
            inboundDate:''
        }
    }
}
</script>

<style lang="scss" scoped>
    .statistical{
        background: transparent !important;
        margin-bottom: 10px;
        padding-right: 30px;
        .model{
            background: white;
            border: 1px solid #e5e5e5;
            div{
                padding-left: 15%;
                padding-top: 10%;
                box-sizing: border-box;
                height: 110px;
                line-height: 60px;
                .title{
                    font-size: 14px;
                    margin-bottom: 10px;
                    color:gray;
                }
                .num{
                   color: black;
                   font-size: 20px;
                   font-family: 'Arial Normal', 'Arial';
                }
            }
        }
    }
    .table{
        background: white;
    }
</style>

