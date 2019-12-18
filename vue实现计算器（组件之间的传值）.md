# vue实现计算器（组件之间的传值）

* caculate.vue 父组件

  ```javascript
  <template>
  <div>
  <Button @handle='dosome'></Button>		
  <br/><el-input
    type="textarea"
    :rows="2"
    placeholder="请输入内容"
    v-model="textarea">
  </el-input>
  </div>
  </template>
  <script>
  import Button from "./Button"
  
  export default {
      name:'Caculate',
      components:{
          Button
      },
      data() {
      return {
        textarea: '',      //结果显示
        temp:'',          //操作数1
        temp2:'',          //操作数2
        flag:''           //操作符
          }
      },
      methods:{
          dosome(data){
               if(data==='clear'){
                         
                   this.clear()
                   return 
               }
               if(data==='='){
                   this.equal()
                   return 
               }
               if(data==='+'||data==='-'||data==='*'||data==='/'){
                   this.buff(this.temp,data)
                   return 
               }
              
              this.temp += data
              this.textarea=this.temp
          },
          buff(operation,flag){
              this.flag=flag
              this.temp2=operation
              this.temp=''
          },
          clear(){            //清空缓存区
              this.textarea=''
              this.temp=''
              this.temp2=''
              this.flag=''
          },
          equal(){            //触发运算
              switch(this.flag){
                  case '+':
                       this.textarea=parseInt(this.temp2)+parseInt(this.temp)
                       this.temp=this.textarea
                       break;
                  case '-':
                       this.textarea=parseInt(this.temp2)-parseInt(this.temp)
                       this.temp=this.textarea
                       break;
                   case '*':
                       this.textarea=parseInt(this.temp2)*parseInt(this.temp)
                       this.temp=this.textarea
                       break;
                   case '/':
                       this.textarea=parseInt(this.temp2)/parseInt(this.temp)
                       this.temp=this.textarea
                       break;
                  default:
                      this.clear()
              }
              //if(this.flag==='+'){}else if(this.flag==='-'){}else if(this.flag)
              //this.textarea=parseInt(this.temp2)+parseInt(this.temp)
             
          }
   }
  }
  </script>
  <style scoped>
  
  </style>
  ```

  

- button.vue 子组件

  ```JavaScript
  <template>
  <div>
      <el-row>
          <el-button @click="$emit('handle',1)" size="">1</el-button>
          <el-button @click="$emit('handle',2)">2</el-button>
          <el-button @click="$emit('handle',3)">3</el-button>
          <el-button @click="$emit('handle','+')" type='info'>+</el-button>
      </el-row>
       <el-row>
          <el-button @click="$emit('handle',4)">4</el-button>
          <el-button @click="$emit('handle',5)">5</el-button>
          <el-button @click="$emit('handle',6)">6</el-button>
          <el-button @click="$emit('handle','-')" type='info'>-</el-button>
      </el-row>
       <el-row>
          <el-button @click="$emit('handle',7)">7</el-button>
          <el-button @click="$emit('handle',8)">8</el-button>
          <el-button @click="$emit('handle',9)">9</el-button>
          <el-button @click="$emit('handle','*')" type='info'>*</el-button>
      </el-row>
      <el-row>
          <el-button @click="$emit('handle','clear')" type='warning'>clear</el-button>
          <el-button @click="$emit('handle',0)">0</el-button>
          <el-button @click="$emit('handle','/')" type='info'>/</el-button>
          <el-button @click="$emit('handle','=')" type='info'>=</el-button>
      </el-row>
      
  </div>
  </template>
  <script>
  export default {
      name:"Button",
      props:['sum'],
      methods:{
              listen:function (e) {
                  this.$emit('listen',e);
                  //this.$parent.age=20
              }
          }
  }
  </script>
  <style scoped>
  
  </style>
  ```

  

