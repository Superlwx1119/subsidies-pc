import Vue from 'vue'
import Router from 'vue-router'
import Home from '@/views/Home'
import Login from '@/views/Login'
import NotFind from '@/views/NotFind'
import Index from '@/views/components/Index/Index'
import GoodsList from '@/views/components/ItemManagement/GoodsList'
import InventoryRecords from '@/views/components/ItemsRecorded/InventoryRecords'
import GoodsDetailIn from '@/views/components/ItemsRecorded/GoodsDetailIn'
import GoodsDetailOut from '@/views/components/ItemsRecorded/GoodsDetailOut'
import GoodsDetailRecycling from '@/views/components/ItemsRecorded/GoodsDetailRecycling'
import GoodsDetailStatistics from '@/views/components/ItemsRecorded/GoodsDetailStatistics'
import OutboundRecords from '@/views/components/ItemsRecorded/OutboundRecords'
import RecyclingRecords from '@/views/components/ItemsRecorded/RecyclingRecords'
import GoodsStatistics from '@/views/components/ItemsRecorded/GoodsStatistics'
import SettingReward from '@/views/components/RewardQuery/SettingReward'
import MyReward from '@/views/components/RewardQuery/MyReward'
import DealeRaward from '@/views/components/RewardQuery/DealeRaward'
import ApprovalRecorded from '@/views/components/GetMoneyApproval/ApprovalRecorded'
import NotApproval from '@/views/components/GetMoneyApproval/NotApproval'
import DealerList from '@/views/components/DealerManagement/DealerList'
import AddDealer from '@/views/components/DealerManagement/AddDealer'
import ResetPassword from '@/views/components/DealerManagement/ResetPassword'
import BasicInformation from '@/views/components/Information/BasicInformation'
import AmountAccount from '@/views/components/Information/AmountAccount'
import CardSettings from '@/views/components/Information/CardSettings'


Vue.use(Router)

const router = new Router({
  routes: [
    {
      path: '/',
      name: '首页',
      // leaf: true,//只有一个节点
      iconCls: 'el-icon-document',
      redirect:'/index',
      component: Home,
      children:[
        { path: '/index', component: Index, name: '首页', meta:{requiresAuth:true}},
      ]
    },
    {
      path: '*',
      hidden: true,
      redirect: { path: '/404' }
    },
    {
      path: '/404',
      component: NotFind,
      name: '',
      hidden: true
    },
    {
      path: '/Login',
      name: 'Login',
      component: Login,
      hidden:true
    },
    {
      path: '/',
      name: '物品管理',
      component: Home,
      iconCls: 'el-icon-document',
      // redirect:'/goodsList',
      children:[
        { path: '/goodsList', component: GoodsList, name: '物品列表', meta:{requiresAuth:true}}//是否进行登录验证,
      ],
      
    },
    {
      path: '/',
      name: '物品记录',
      component: Home,
      iconCls: 'el-icon-edit-outline',
      children:[
        { path: '/inventoryRecords', component: InventoryRecords, name: '入库记录', meta:{requiresAuth:true},children:[{path:'/GoodsDetailIn',component:GoodsDetailIn,name:'物品明细',hidden:true,meta:{requiresAuth:true}}]},
        { path: '/outboundRecords', component: OutboundRecords, name: '出库记录', meta:{requiresAuth:true},children:[{path:'/GoodsDetailOut',component:GoodsDetailOut,name:'物品明细',hidden:true,meta:{requiresAuth:true}}]},
        { path: '/recyclingRecords', component: RecyclingRecords, name: '回收记录', meta:{requiresAuth:true},children:[{path:'/GoodsDetailRecycling',component:GoodsDetailRecycling,name:'物品明细',hidden:true,meta:{requiresAuth:true}}]},
        { path: '/goodsStatistics', component: GoodsStatistics, name: '物品统计', meta:{requiresAuth:true},children:[{path:'/GoodsDetailStatistics',component:GoodsDetailStatistics,name:'物品明细',hidden:true,meta:{requiresAuth:true}}]},
      ]
    },
    {
      path: '/',
      name: '奖励查询',
      component: Home,
      iconCls: 'el-icon-view',
      children:[
        { path: '/myReward', component: MyReward, name: '我的奖励', meta:{requiresAuth:true}},
        { path: '/DealeRaward', component: DealeRaward, name: '经销商奖励', meta:{requiresAuth:true}},
        { path: '/settingReward', component: SettingReward, name: '奖励设置', meta:{requiresAuth:true}},
      ]
    },
    {
      path: '/',
      name: '提现审批',
      component: Home,
      iconCls: 'el-icon-bell',
      children:[
        { path: '/NotApproval', component: NotApproval, name: '待审批', meta:{requiresAuth:true}},
        { path: '/ApprovalRecorded', component: ApprovalRecorded, name: '审核记录', meta:{requiresAuth:true}},
      ]
    },
    {
      path: '/',
      name: '经销商管理',
      component: Home,
      iconCls: 'el-icon-document',
      children:[
        { path: '/DealerList', component: DealerList, name: '经销商列表', meta:{requiresAuth:true}},
        { path: '/AddDealer', component: AddDealer, name: '新增经销商', meta:{requiresAuth:true}},
        { path: '/ResetPassword', component: ResetPassword, name: '重置密码', meta:{requiresAuth:true}},
      ]
    },
    {
      path: '/',
      name: '基本信息',
      component: Home,
      iconCls: 'el-icon-edit',
      children:[
        { path: '/BasicInformation', component: BasicInformation, name: '基本资料', meta:{requiresAuth:true}},
        { path: '/AmountAccount', component: AmountAccount, name: '账户金额', meta:{requiresAuth:true}},
        { path: '/CardSettings', component: CardSettings, name: '银行卡设置', meta:{requiresAuth:true}},
      ]
    },
  ]
})

router.beforeEach((to, from, next) => {    
  //to即将进入的目标路由对象，from当前导航正要离开的路由， next  :  下一步执行的函数钩子
if(to.path === '/Login')  {
 var timer=null
 if(sessionStorage.getItem('token')){
//   		alert('已登录,无需再登录');
   timer=setInterval(()=>{
     next({ path: '/' })
   },10)
 }
 next()
 }  // 如果即将进入登录路由，则直接放行
else {     //进入的不是登录路由
    if(to.meta.requiresAuth && !sessionStorage.getItem('token')) {next({ path: '/Login' })} 
    //下一跳路由需要登录验证，并且还未登录，则路由定向到  登录路由
    else { next() }}  //如果不需要登录验证，或者已经登录成功，则直接放行
});
export default router;
