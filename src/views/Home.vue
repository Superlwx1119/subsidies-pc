<template>
    <el-row class="container">
        <el-col :span="24" class="header">
			<el-col :span="10" class="logo" :class="collapsed?'logo-collapse-width':'logo-width'">
				{{collapsed?'':sysName}}
			</el-col>
			<el-col :span="10" class="header_right">
				<div class="tools" @click.prevent="collapse">
					<i class="el-icon-menu"></i>
				</div>
			</el-col>
			<el-col :span="4" class="userinfo">
				<el-dropdown trigger="hover">
					<span class="el-dropdown-link userinfo-inner"><img src="../assets/images/touxiang.png" /> {{sysUserName|sysUserName}}</span>
					<el-dropdown-menu slot="dropdown">
						<!-- <el-dropdown-item>我的消息</el-dropdown-item> -->
						<el-dropdown-item @click.native="changePassword">修改密码</el-dropdown-item>
						<el-dropdown-item divided  @click.native="logout">退出登录</el-dropdown-item>
					</el-dropdown-menu>
				</el-dropdown>
			</el-col>
		</el-col>
		<el-col :span="24" class="main">
			<aside :class="collapsed?'menu-collapsed':'menu-expanded'">
				<!--导航菜单-->
				<el-menu  :default-active="$route.path" class="el-menu-vertical-demo" @open="handleopen" @close="handleclose" @select="handleselect"
					 unique-opened router v-show="!collapsed">
					<template v-for="(item,index) in $router.options.routes"  v-if="!item.hidden" >
						<el-submenu :index="index+''" v-if="!item.leaf" >  
							<template slot="title"><i :class="item.iconCls"></i>{{item.name}}</template>
							<el-menu-item v-for="child in item.children" :index="child.path" :key="child.path" v-if="!child.hidden">{{child.name}}</el-menu-item>
						</el-submenu>
						<el-menu-item v-if="item.leaf&&item.children.length>0" :index="item.children[0].path"><i :class="item.iconCls"></i>{{item.children[0].name}}</el-menu-item>
					</template>
				</el-menu>
				<!--导航菜单-折叠后-->
				<ul class="el-menu el-menu-vertical-demo collapsed" v-show="collapsed" ref="menuCollapsed">
					<li v-for="(item,index) in $router.options.routes" :key="index" v-if="!item.hidden" class="el-submenu item">
						<template v-if="!item.leaf">
							<div class="el-submenu__title" style="padding-left: 20px;" @mouseover="showMenu(index,true)" @mouseout="showMenu(index,false)"><i :class="item.iconCls"></i></div>
							<ul class="el-menu submenu" :class="'submenu-hook-'+index" @mouseover="showMenu(index,true)" @mouseout="showMenu(index,false)"> 
								<li v-for="child in item.children" v-if="!child.hidden" :key="child.path" class="el-menu-item" style="padding-left: 40px;" :class="$route.path==child.path?'is-active':''" @click="$router.push(child.path)">{{child.name}}</li>
							</ul>
						</template>
						<template v-else>
							<li class="el-submenu">
								<div class="el-submenu__title el-menu-item" style="padding-left: 20px;height: 56px;line-height: 56px;padding: 0 20px;" :class="$route.path==item.children[0].path?'is-active':''" @click="$router.push(item.children[0].path)"><i :class="item.iconCls"></i></div>
							</li>
						</template>
					</li>
				</ul>
			</aside>
			<section class="content-container">
				<div class="grid-content bg-purple-light">
					<el-col :span="24" class="breadcrumb-container" v-if="$route.path!='/index'">
						<!-- <strong class="title">{{$route.name}}</strong> -->
						<el-breadcrumb separator="/" class="breadcrumb-inner">
							<el-breadcrumb-item v-for="item in $route.matched" :key="item.path">
								{{ item.name }}
							</el-breadcrumb-item>
						</el-breadcrumb>
					</el-col>
					<el-col  :span="24" class="content-wrapper">
						<transition name="fade" mode="out-in">
							<router-view></router-view>
						</transition>
					</el-col>
				</div>
			</section>
		</el-col>
        <!-- <router-view/> -->
    </el-row>
    
</template>

<script>
import Qs from 'qs'
import axios from 'axios'
import store from '@/store';
export default {
	name:'Home',
	filters:{
		sysUserName(val){
			return val+',欢迎登陆!'
		}
	},
    data(){
        return{
            collapsed:false,
            sysName:'补贴购代理管理平台',
			sysUserName:'admin',
			newPass:'',
			oldPass:'11',
			newPassAgin:''
        }
	},
	methods:{
		logout(){
			//登出
			this.$confirm('确定是否退出当前用户?', '提示', {
				confirmButtonText: '确定',
				cancelButtonText: '取消',
				type: 'warning'
			}).then(()=>{
				store.dispatch('userLogout')
				this.$router.push('/Login')
			})
		},
		changePassword(){
			const h = this.$createElement;
            this.$msgbox({
                title: '修改密码',
                center:'true',
                message: h('form', {style:{textAlign:'center'}}, [
					h('p',{style:{width:'300px',display:'flex',alignItems:'center'}},[h('span',{style:{display:'block',width:'100px'}},'旧密码'),h('el-input',{props:{value:this.oldPass},attrs:{placeholder:'请输入旧密码',type:'password'}})]),
					h('p',{style:{width:'300px',display:'flex',alignItems:'center',margin:'20px 0'}},[h('span',{style:{display:'block',width:'100px'}},'新密码'),h('el-input',{props:{value:this.newPass},attrs:{placeholder:'请输入新密码',type:'password'}})]),
					h('p',{style:{width:'300px',display:'flex',alignItems:'center'}},[h('span',{style:{display:'block',width:'100px'}},'确认新密码'),h('el-input',{props:{value:this.newPassAgin},attrs:{placeholder:'请再次输入新密码',type:'password'}})]),
                ]),
                showCancelButton: true,
                confirmButtonText: '确认修改',
                cancelButtonText: '取消',
                // beforeClose: (action, instance, done) => {
                //     if (action === 'confirm') {
                //     instance.confirmButtonLoading = true;
                //     instance.confirmButtonText = '执行中...';
                //     setTimeout(() => {
                //         done();
                //         setTimeout(() => {
                //         instance.confirmButtonLoading = false;
                //         }, 300);
                //     }, 3000);
                //     } else {
                //     done();
                //     }
                // }
            }).then(action => {
				if(action==='confirm'){
					console.log(this.oldPass)
				}
                this.$message({
                    type: 'info',
                    message: 'action: ' + action
                });
            });
		},
		handleopen() {
			// console.log('handleopen');
		},
		handleclose() {
			//console.log('handleclose');
		},
		handleselect(a, b) {
			store.dispatch('showDetail',false)
		},
		collapse(){
			//缩小导航
			this.collapsed=!this.collapsed;
			if(this.collapsed){
				$('.container .main aside .el-menu[data-v-fae5bece]').css('width','60px')
			}else{
				$('.container .main aside .el-menu[data-v-fae5bece]').css('width','230px')
			}
		},
		showMenu(i,status){
			this.$refs.menuCollapsed.getElementsByClassName('submenu-hook-'+i)[0].style.display=status?'block':'none';
		}
	},
	mounted(){
		// console.log(this.$route.path)
		this.sysUserName=this.$store.state.token
	}
}
</script>

<style scoped lang="scss">
	.container {
		position: absolute;
		top: 0px;
		bottom: 0px;
		width: 100%;
		.header {
			height: 60px;
			line-height: 60px;
            background: #fff;
            border-bottom: 1px solid #e9e9e9;
            color:#fff;
			.userinfo {
				text-align: right;
				padding-right: 35px;
				float: right;
				.userinfo-inner {
					cursor: pointer;
					color:gray;
					img {
						width: 40px;
						height: 40px;
						border-radius: 20px;
						margin: 10px 0px 10px 10px;
						float: right;
					}
				}
			}
			.logo {
                //width:230px;
                background: #00284c;
				height:60px;
				font-size: 16px;
				padding-left:20px;
				padding-right:20px;
				border-color: rgba(238,241,146,0.3);
				border-bottom-width: 1px;
				border-bottom-style: solid;
				img {
					width: 40px;
					float: left;
					margin: 10px 10px 10px 18px;
				}
				.txt {
					color:#fff;
				}
			}
			.logo-width{
				width:230px !important;
			}
			.logo-collapse-width{
				width:60px
			}
			.tools{
				padding: 0px 23px;
                width:14px;
                font-size: 24px;
                color: gray;
				height: 60px;
				line-height: 60px;
                cursor: pointer;
			}
		}
		.main {
			display: flex;
			// background: #324057;
			position: absolute;
			top: 60px;
			bottom: 0px;
			overflow: hidden;
			aside {
				flex:0 0 230px;
				width: 230px;
				background: #001428 !important;
				// position: absolute;
				// top: 0px;
				// bottom: 0px;
				.el-menu{
					height: 100%;
					background: #001428 !important;
				}
				.collapsed{
					width:60px;
					.item{
						position: relative;
					}
					.submenu{
						position:absolute;
						top:0px;
						left:60px;
						z-index:99999;
						height:auto;
						display:none;
						
					}

				}
			}
			.menu-collapsed{
				background: #001428 !important;
				flex:0 0 60px;
				width: 60px;
			}
			.menu-expanded{
				background: #001428 !important;
				flex:0 0 230px;
				width: 230px !important;
			}
			.content-container {
				overflow-x: hidden;
				background: #f1f3f5;
				flex:1;
				// position: absolute;
				// right: 0px;
				// top: 0px;
				// bottom: 0px;
				// left: 230px;
				overflow-y: auto;
				// padding: 20px;
				.breadcrumb-container {
					height: 50px;
					padding-left:20px;
					background: white;
					border-bottom: 1px solid #e5e5e5;
					line-height: 50px;
					//margin-bottom: 15px;
					.title {
						width: 200px;
						float: left;
						color: #475669;
					}
					.breadcrumb-inner {
						// float: left;
						height: 50px;
						line-height: 50px;
					}
				}
				.content-wrapper {
					margin: 10px;
					// background-color: #fff;
					box-sizing: border-box;
				}
			}
		}
	}
</style>

