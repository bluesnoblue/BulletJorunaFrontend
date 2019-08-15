<template>
  <div class="hello">
    <el-container>
      <el-menu 
        default-active="1-4-1" 
        class="el-menu-vertical-demo" 
        @open="handleOpen" 
        @close="handleClose" 
        :collapse="isCollapse">
        <el-menu-item>
          <template>
                  <i class="el-icon-news"></i>
                  <span slot="title">未完成</span>
          </template>
        </el-menu-item>
        <el-menu-item>
          <template>
                  <i class="el-icon-location"></i>
                  <span slot="title">本日任务</span>
          </template>
        </el-menu-item>
        <el-menu-item>
          <template>
                  <i class="el-icon-date"></i>
                  <span slot="title">本月任务</span>
          </template>
        </el-menu-item>
        <el-menu-item>
          <template>
                  <i class="el-icon-date"></i>
                  <span slot="title">年度任务</span>
          </template>
        </el-menu-item>
      </el-menu>
      
      <el-main>
        <div>
          <el-button icon="el-icon-more" sharp style='float:left' @click="isCollapse = !isCollapse"></el-button>
          <el-date-picker 
            v-model="select_time" 
            type="date" 
            placeholder="选择日期"
            value-format="timestamp"
            >
            </el-date-picker>
          <el-button 
            icon="el-icon-user-solid" 
            circle 
            style='float:right'
            @click='drawer=true'
            type='primary'
            ></el-button>
        </div>
        <div>
          <h1>title</h1>
          <el-card :key='bullet.id' class='bullet' v-for='bullet in bullets'>
          {{bullet.content}}
          </el-card>
        </div>

        <div class='plues'>
          <el-button type="primary" icon="el-icon-s-opportunity" circle @click="postBullet"></el-button>
          <el-button type="primary" icon="el-icon-s-promotion" circle></el-button>
          <el-button type="primary" icon="el-icon-plus" circle ></el-button>
        </div>

        <el-drawer 
        :visible.sync='drawer'
        :direction='rt1'
        class='user_page'>
          <div>
            <h1>{{user.name}}</h1>
            <div>mobile: {{user.mobile}}</div>
            <div>email: {{user.email}}</div>
            <el-button class="logout_button" type="danger" round=false>退出登录</el-button>
          </div>

        </el-drawer>

      </el-main>
    </el-container>
  </div>
</template>

<script>
export default {
  name: 'index',
  data () {
    return {
      isCollapse: true,
      select_time: '',
      bullets: [{
        'id':1,
        'content': 'testtext',
        'time': 1565026283,
        'type': 1
        },{
        'id':2,
        'content': 'testtext2',
        'time': 1565026284,
        'type': 1
         }],
      user:{
        'id':1,
        'name':'TestUser',
        'mobile':'1234567901',
        'email':'test@mail.com',
      },
      drawer: false
    }
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
    postBullet() {
        this.$prompt('请输入内容', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
        }).then(({ value }) => {
          this.$message({
            type: 'success',
            message: '你的邮箱是: ' + value
          });
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
/* ul {
  list-style-type: none;
  padding: 0;
}
li{
  display: inline-block;
  margin: 0;
  padding: 16px 0;
  border: 0;
  display: block;
  overflow: hidden;
}
a {
  color: #42b983;
} */

  .el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 200px;
    min-height: 400px;
  }

.el-aside{
  min-height: 100vh;
  background-color: #eee;
  width: 200px;
}

.el-main{
  min-height: 100vh;
}
.bullet{
  display:flex;
}
.plues{
  position:fixed;
  bottom:5vh;
  right:5vh;
}
.user_page{
  text-align:center;
}
.logout_button{
  position:fixed;
  bottom: 5vh;
  right:5%
}
</style>
