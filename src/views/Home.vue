<template>
  <div class="home">
    <!-- 头部 -->
      <div class="header">
        <h5>全选<input type="checkbox" @click="all" v-model="mo" ></h5>
        <button @click='changegg'>修改</button>
        <button @click="revi">删除</button>
        <button @click="fage=true">添加</button>   
      </div>
    <!-- 列表 -->
      <div>
        <ul>
          <li v-for='(item,index) in List' 
              :key='item.age'
              >
            <input type="checkbox" v-model='check[index]'  @click="zaoqi"  class="active" >
            {{item.usecname}}
          </li>
        </ul>

      </div>
    <!-- 添加布局 -->
       <div class="ban" v-show="fage">
         姓名<input type="text" ref='a'><br/>
           账号<input type="text" v-lenth='fun' v-model="a"
                @click="spa=true"
                ref='b'
                >
                  <span v-show="spa">{{text}}</span><br/>
            密码<input type="text" v-next='fnu'    v-model="b"   @click="spe=true"
                 ref='c'
            >
                  <span v-show='spe'>{{tit}}</span>
            <br/>
              爱好<input type="text"
                 ref="d"
              ><br/>
               性别<input type="text"
                 ref='e'
               ><br/>
                 年龄<input type="text"
                  ref="f"
                  v-model="yanzheng"
                  v-color
                 ><br/>
                  介绍<input type="text"
                  ref="g"
                  ><br/>

                  <h2>
                    <p @click="change">添加</p>  <p @click="fage=false">取消</p>
                  </h2>
       </div>
       <!-- 修改 -->
    <div v-show='gg' class="boo" ref='boo'>
        姓名<input type="text" ref='h'><br/>
         账号<input type="text" ref='i'><br/>
          密码<input type="text" ref='j'><br/>
           爱好<input type="text" ref='k'><br/>
          
             性别<input type="text" ref='l'><br/>
              年龄<input type="text" ref='m'><br/>
               介绍<input type="text" ref='n'><br/>
               <h2><p @click="sheep">确认</p><p @click="gg=false">取消</p></h2>
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return{
      yanzheng:'',
      gg:false,
      List:[
        { 
          usecname:'哪吒',
          usec:9526,
          password:'santaizi',
          loves:'吃饭',
          sex:'男',
          age:7,
          Resume:'年轻的时候闹过海，自杀过，后来当神仙了'
        },
        { 
          usecname:'齐天大圣',
          usec:9527,
          password:'wukong',
          loves:'打妖怪',
          sex:'男',
          age:500,
          Resume:'年轻的时候闹过天宫，被压过，后来成佛了'
        },
      ],
      check:[false,false],
      fage:false,
      a:'',
      b:'',
      mo:false,
      spa:false,
      spe:false,
      text:'请输入3位以上字符',
      tit:'请输入不重复的2位以上',
      num:0
   
    }
  },
     
  methods:{
   fun(res){
     this.text=res
   },
   fnu(res){
      this.tit=res
   },
   change(){
      if(!(this.text==''&& this.tit=='')){
           alert('按照规范OK？')
           return
     }
     this.fage=false
    
         this.List.push({
          usecname:this.$refs.a.value,
          usec:this.$refs.b.value,
          password:this.$refs.c.value,
          loves:this.$refs.d.value,
          sex:this.$refs.e.value,
          age:this.$refs.f.value,
          Resume:this.$refs.g.value
         })
         
           this.check.push(this.mo)
        
       /*   this.check.push(false) */
         for(let key in this.$refs){
           this.$refs[key].value=''
         }
        this.a=''
        this.b=''
         
   },
   revi(){
     
         const arr1= this.check.filter((item)=>{
           return item==true
      })
          if(arr1.length==0){
            alert('删除空气？ 请选中')
            return
          }
    /*  const index=this.check.findIndex((item)=>{
            return item==true
            
      })
         if(index!=-1){
            this.List.splice(index,1)
            this.check.splice(index,1)
            
         }
           console.log(this.check);
         */

        for(var i=0; i<this.check.length;i++){
          if(this.check[i]==true){
               this.List.splice(i,1)
            this.check.splice(i,1)
            i--
          }
        }
         if(this.check.length==0){
          this.mo=false
        }
       
   },
   all(){
        for(var i=0;i<this.check.length;i++){
          this.check[i]=!this.mo
        }
   },
   changegg(){
       
      const arr1= this.check.filter((item)=>{
           return item==true
      })
        if(arr1.length>1){
          alert('一条一条修改ok？')
          return
        }else if(arr1.length==0){
          alert('修改了个寂寞 请选中')
          return
        }

     this.gg=true
      const index=this.check.findIndex((item)=>{
            return item==true
            
      })
      const arr=this.List[index]
         
         this.$refs.h.value=arr.usecname
         this.$refs.i.value=arr.usec
         this.$refs.j.value=arr.password
         this.$refs.k.value=arr.loves
         this.$refs.l.value=arr.sex
         this.$refs.m.value=arr.age
         this.$refs.n.value=arr.Resume
        
        
   },
   sheep(){
      this.gg=false
      const index=this.check.findIndex((item)=>{
            return item==true
            
      })
      this.List[index].usecname=this.$refs.h.value
      
        this.List[index].usec= this.$refs.i.value
         this.List[index].sex=this.$refs.j.value
         this.List[index].password=this.$refs.k.value
         this.List[index].loves=this.$refs.l.value
         this.List[index].age=this.$refs.m.value
         this.List[index].Resume=this.$refs.n.value
   },
   zaoqi(){
      this.num=document.getElementsByClassName('active')
      let arr=[]
          this.num.forEach((item)=>{
                 arr.push(item)
          })
      this.mo =   arr.every((item)=>{
            return item.checked==true
         })
         
         
         
   }
  },
  directives:{
    lenth:{
      componentUpdated(el,bind){
       
       
         if(el.value.length<3){
           bind.value('请输入3位以上字符')
            
            
        }else{
          bind.value('')
        }
        
        
        
      }
    },
    next:{
     componentUpdated(el,bind){
            let rig=false
         let arr=el.value.split('')
           for(let i=1;i<arr.length;i++){
                if(arr[0]!=arr[i]){
                    rig=true
                }
           }
          
           
           if(rig){
             bind.value('')
             
           }else{
             bind.value('请输入不重复的2位以上')
             
           }
       
        
        
      }
    },
    color:{
      componentUpdated(el){
          
            let arr = el.value.trim()-0
               let a =   /^\d{1,3}$/
            let b=    a.test(arr)
               if(!b){
                 el.style.color='red'
               }else{
                  el.style.color='#555'
               }
                
         
             
      }
    }
  },
  mounted(){
     console.log(this.$refs.boo.children);
  
     
  }
}
</script>
<style lang="scss" scoped>
 *{
   margin: 0;
   padding: 0;
   box-sizing: border-box;
 }
.header{
  width: 100%;
  height: 60px;
  background: red;
  padding: 0 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;

}
.ban{
    width: 100%;
    height:50% ;
    position: absolute;
    background-color: red;
    top: 0;
    left: 0;
    padding-top: 30px;
    h2{
      display: flex;
      padding: 0 10px;
      justify-content:space-around;
      margin-top: 10px;
    }
  }
  .boo{
    width: 100%;
    height:50% ;
    position: absolute;
    background-color: red;
    top: 0;
    left: 0;
    padding-top: 30px;
     h2{
      display: flex;
      padding: 0 10px;
      justify-content:space-around;
      margin-top: 10px;
    }
  }
</style>
