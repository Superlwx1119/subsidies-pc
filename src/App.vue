<template>
  <div id="app">
    <transition name="fade"
		            mode="out-in">
			<router-view></router-view>
		</transition>
  </div>
</template>

<script>
export default {
  name: 'App',
  components:{
  }
}
</script>

<style lang='scss'>
    *{
      padding: 0;
      margin: 0;
      list-style: none;
    }
    body {
	margin: 0px;
	padding: 0px;
	/*background: url(assets/bg1.jpg) center !important;
		background-size: cover;*/
	// background: #1F2D3D;
	font-family: Helvetica Neue, Helvetica, PingFang SC, Hiragino Sans GB, Microsoft YaHei, SimSun, sans-serif;
	font-size: 14px;
	-webkit-font-smoothing: antialiased;
}

#app {
	position: absolute;
	top: 0px;
	bottom: 0px;
	width: 100%;
}

.el-submenu [class^=fa] {
	vertical-align: baseline;
	margin-right: 10px;
}

.el-menu-item [class^=fa] {
	vertical-align: baseline;
	margin-right: 10px;
}

.toolbar {
	background: #f2f2f2;
	padding: 10px;
	//border:1px solid #dfe6ec;
	margin: 10px 0px;
	.el-form-item {
		margin-bottom: 10px;
	}
}

.fade-enter-active,
.fade-leave-active {
	transition: all .2s ease;
}

.fade-enter,
.fade-leave-active {
	opacity: 0;
}
.el-table--border td, .el-table--border th, .el-table__body-wrapper .el-table--border.is-scrolling-left~.el-table__fixed{
	border-right: none !important;
}
.el-input__inner{
	width: 180px;
}
.index{
	.el-input__inner{
		width: 200px;
		height: 30px;
		line-height: 30px;
	}
	.el-input__icon{
		line-height: 0px;
	}
	.el-date-editor.el-input, .el-date-editor.el-input__inner{
		width: 200px;
	}
	.el-carousel__arrow:hover{
		background: rgba(31,45,61,.6)
	}
	.el-carousel__arrow{
		background: rgba(31,45,61,.35)
	}
	.el-carousel__container{
		height: 200px !important;
	}
}
.login {
	.el-input__inner{
		background: transparent;
		border: none;
		outline: none;
		font-size: 16px !important;
		color: white;
	}
	.el-button{
		background: #dd9f1b;
		width: 300px;
		color: white;
		font-size: 16px;
		border: none;
	}
	.el-form-item__error{
		left:32% !important;
		color: red;
	}
	.el-message-box__content .title{
		width: 70px;
		display: inline-block;
	}
}
// .container .main aside .el-menu[data-v-fae5bece]{
// 	width: 230px !important;
// }
.el-submenu .el-menu-item:hover, .el-submenu__title:hover{
	background: #0a3866 !important;
}
.el-submenu__title{
	color: white;
}
.el-submenu .el-menu-item{
	color: #838d97;
	background: #001428 !important;
}
.el-menu-item.is-active{
	background: #0a3866 !important;
}
// .el-menu-vertical-demo{
// 	width: 230px !important;
// }
</style>
