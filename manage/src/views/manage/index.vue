<template>
  <div class="manage tc">
    <button v-on:click="add">新增</button>
    <div class="input-area" v-show="showAdd">
      <input type="text" placeholder="请输入人员姓名" v-model="addName">
      <button v-on:click="insert">确定</button>
    </div>
    <table>
      <tr>
        <th>序号</th>
        <th>姓名</th>
        <th>操作</th>
      </tr>
      <tr v-for="(p,i) in person">
        <td>{{i}}</td>
        <td>{{p.name}}</td>
        <td v-bind:id="i"><span v-on:click="edit">编辑</span><span v-on:click="del">删除</span></td>
      </tr>
    </table>
    <div class="wrap" v-show="showEdit">
      <div class="content">
        <input type="text" placeholder="请输入新姓名" v-model="newName"/>
        <button v-on:click="cancel">取消</button>
        <button v-on:click="confirm">确定</button>
      </div>

    </div>
    <footer-nav :class="{'isManage':isNowPage}"></footer-nav>
  </div>
</template>

<script>
  import FooterNav from '../../components/footer.vue'
    export default {
        components: {
          FooterNav
        },
        data(){
          return {
            person: [
              {
                name: "练宏",
              },
              {
                name: "脸红"
              }
            ],
            addName: "",
            isNowPage: true,
            showAdd: false,
            newName: "",
            showEdit: false,
            editId: 0
          }
        },
      methods: {
          add(){
            this.showAdd = true;
          },
          insert(){
            const data = {};
            const v = this.addName;
            if(v.trim()==""){
              alert("名字不能为空，请输入新增人员姓名!!!");
              return;
            }
            data.name = v;
            this.person.push(data);
            this.addName = "";
            this.showAdd = false;
          },
          del(e){
            var id = e.target.offsetParent.id;
            console.info("========",e.target.offsetParent);
            this.person.splice(id,1)
          },
          edit(e){
            var id = e.target.offsetParent.id;
            this.showEdit = true;
            this.editId = id;
            this.newName = this.person[id].name;
          },
          cancel(){
            this.showEdit = false;
          },
          confirm(){
            var v = this.newName;
            if(v.trim()==""){
              alert("名字不能为空，请输入人员姓名!!!");
              return;
            }
            this.person[this.editId].name = this.newName;
            this.showEdit = false;
          }
      }
    }
</script>

<style scoped>
  .manage{padding-bottom:50px;}
  .manage >button{width:200px; height:40px; line-height:40px; background-color:#41b883; border: none; border-radius:5px; font-size:16px; color:#fff;}
  table{width:100%; max-width:500px; margin:0 auto; margin-top:20px;}
  .input-area input{width: 200px; height: 40px; line-height:40px; margin:20px 0; outline:none; border:1px solid #333;}
  .input-area button{ width:60px; height: 40px; line-height:40px; background-color:#41b883; border: none; border-radius:5px; font-size:16px; color:#fff;}
  th,td{width:100px;}
  tr input{width:100px; height:30px; padding-left:10px; outline:none; border:1px solid #333;}
  .wrap{display:table; position:fixed; top:0; left:0; height:100%; width:100%; background:rgba(0,0,0,.8); z-index: 10;}
  .wrap .content{display:table-cell; vertical-align:middle;}
  .wrap .content input{height: 40px; line-height: 40px; display:block; margin:0 auto; margin-bottom:10px; font-size:16px;}
  .wrap .content button{width:100px; height: 30px; line-height: 30px; background-color:#41b883; border: none; border-radius:5px; font-size:16px; color:#fff;}
</style>
