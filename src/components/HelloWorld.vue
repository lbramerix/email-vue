<template>
   <div>
     <div class="top_div"></div>
     <div style="background: rgb(255, 255, 255); margin: -130px auto auto; border: 1px solid rgb(231, 231, 231); border-image: none; width: 1000px; height: 224px; text-align: center;">
       <p style="padding: 30px 0px 10px; position: relative;"><span
         class="u_logo"></span>
         <input id="loginName" class="ipt" type="email" v-model="email" placeholder="请输入邮箱地址" value="">
         <input class="ipt" id="password" type="text" v-model="title" placeholder="请输入邮件标题" value="">
       </p>

       <el-card style="height: 450px;">
         <quill-editor v-model="content" ref="myQuillEditor" style="height: 500px;" :options="editorOption">
         </quill-editor>
       </el-card>
       <div style="height: 50px; line-height: 50px; margin-top: -4px;background:#fff; border-top-color: rgb(231, 231, 231); border-top-width: 1px; border-top-style: solid;">

         <span style="float: right;">
              <a id="loginBtn" @click="send()">发送</a>
           </span></div>

     </div>

   </div>
</template>

<script>
import {
  quillEditor
} from 'vue-quill-editor'
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'
export default {
  name: 'HelloWorld',
  data () {
    return {
      email: "",
      title:"",
      content:"",
      editorOption: {}
    }
  },
  components: {
    quillEditor
  },
  methods:{
    send: function(){

      //验证邮箱
      var myReg=/^[a-zA-Z0-9_-]+@([a-zA-Z0-9]+\.)+(com|cn|net|org)$/;

      if(myReg.test(this.email)){
        this.$axios.post("email", {

          "email":this.email,
          "title":this.title,
          "content":this.content

        }).then( res => {
          alert(res.data.message)
        }).catch( res => {
          alert(res.data.message)
        })
      }else {
        alert("邮箱格式不对!");
      }

    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  body{
    background: #ebebeb;
    font-family: "Helvetica Neue","Hiragino Sans GB","Microsoft YaHei","\9ED1\4F53",Arial,sans-serif;
    color: #222;
    font-size: 12px;
  }
  *{padding: 0px;margin: 0px;}
  .top_div{
    background: #e7ddc0;
    width: 100%;
    height: 160px;
  }
  .ipt{
    border: 1px solid #d3d3d3;
    padding: 10px 10px;
    width: 420px;
    border-radius: 4px;
    padding-left: 35px;
    -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075);
    box-shadow: inset 0 1px 1px rgba(0,0,0,.075);
    -webkit-transition: border-color ease-in-out .15s,-webkit-box-shadow ease-in-out .15s;
    -o-transition: border-color ease-in-out .15s,box-shadow ease-in-out .15s;
    transition: border-color ease-in-out .15s,box-shadow ease-in-out .15s
  }
  .ipt:focus{
    border-color: #66afe9;
    outline: 0;
    -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6);
    box-shadow: inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6)
  }
  a{
    text-decoration: none;
  }
  #loginBtn {
    margin-right: 30px;
    background: rgb(50, 168, 84);
    padding: 7px 10px;
    border-radius: 4px;
    border: 1px solid rgb(50, 168, 84);
    border-image: none;
    color: rgb(255, 255, 255);
    font-weight: bold;
    cursor: pointer;
  }
</style>
