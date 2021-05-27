<template>
		<div class="header_nav">
			<div>
        <p>欢迎来到有好物</p>
      </div>
			<ul>
				<li v-if="!userInfo.id">
					<router-link to="/login">您好,请登录</router-link>
          <router-link to="/register">免费注册</router-link>
				</li>
				<li v-else>
					<a v-if="userInfo.user_nickname">您好,{{ userInfo.user_nickname }}</a>
          <a v-else>您好,{{ userInfo.user_name | nameFormat }}</a>
					<a @click="headerLogout">退出登录</a>
				</li>
        <li v-if="this.$route.path.indexOf('/home') === -1"><router-link to="/home">返回首页</router-link></li>
				<li><a @click.prevent="goMe">个人中心</a></li>
        <li><a @click.prevent="goShopCar">我的购物车</a></li>
			</ul>
		</div>
</template>

<script>
  import {mapState} from 'vuex';
  import {mapActions} from 'vuex'
  import { MessageBox } from 'element-ui';
  export default {
    data(){
      return{}
    },
    mounted() {},
    computed: {
        ...mapState(["userInfo"])
    },
    methods:{
      ...mapActions(["logOut"]),

      handleAreaChange(value) {
        //console.log(this.selectedOptions);
      },
     
      headerLogout(){
        this.$confirm('您确定退出登录吗?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.$message({
          type: 'success',
          message: '退出成功!'
          });
          let result = this.logOut({});
          window.localStorage.removeItem("userInfo");
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消退出'
          });
        });
      },
      goMe(){
        if(this.userInfo.id){
          this.$router.replace('/me');
        }else{
          MessageBox({
            type: 'info',
            message: "请先登录!",
			      showClose: true,
          });
        }
      },
      goAdmin(){
        let result = window.localStorage.getItem("adminInfo");
        if(result){
          this.$router.replace('/admin');
        }else{
          this.$router.replace('/adminlogin');
        }
      },
      goShopCar(){
        if(this.userInfo.id){
          this.$router.replace('/shopcar');
        }else{
          MessageBox({
            type: 'info',
            message: "请先登录!",
			      showClose: true,
          });
        }
      },
    },
  }
</script>

<style scoped>
/*头部导航*/
.header_nav{
	width: 100%;
	height: 30px;
	background: #F2F2F2;
	font-family:  "Microsoft YaHei";

  display: flex;
  align-items: center;
  justify-content: space-between;
}
.header_nav>div{
  display: flex;
  align-items: center;
}
.header_nav>div p{
	margin: 0 30px 0 20px;
	color: #999;
	font-size: 15px;
}
.locationWrapper{
  position: relative;
  max-width: 100px;

  display: flex;
  align-items: center;

}
.locationWrapper .el-cascader{
  position: absolute;
  opacity: 0;
}
.locationWrapper .address{
  max-width: 58px;
  font-size: 12px;
  color: #999;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  vertical-align: middle;
}
.locationWrapper .icon{
  margin: 0 3px;
  width: 15px;
  height: 15px;
  vertical-align: middle;
}
.locationWrapper .icon path{
  fill: #dd6161;
}
.header_nav>ul{
	margin: 0 50px;
	list-style: none;

  display: flex;
  align-items: center;
}
.header_nav>ul>li:first-child{
	font-size: 14px;
	color:red;
	line-height: 20px;
	cursor: pointer;
}
.header_nav>ul>li>a{
	display: inline-block;
	padding: 5px 15px;
	font-size: 12px;
	line-height: 20px;
	color: #999;
	text-decoration: none;
	cursor: pointer;
}
.header_nav>ul>li>a:hover{
	color: red;
}
.header_nav>ul>li:first-child>a:nth-child(2){
	padding-left: 0;
	color: red;
}
</style>
