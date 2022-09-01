<template>
  <div class="p-3" style="max-width:400px; margin:50px auto; background:#234">
    <h1 class="text-center" style="color:white">CALCULATOR</h1>
    <!-- calculator value -->
    <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vu-dark">
      {{calculatorValue || 0}}
    </div>

    <!-- Calculator button -->
    <div class="row no-gutters">
      <div class="col-3" v-for="n in calculateorEle" :key="n">
        <div class="lead text-white text-center py-3 bg-vu-dark m-1 rounded hover-class"
        :class="{'bg-vue-green': ['C','*','/','-','+','%','= '].includes(n)}"
        @click="action(n)">
          {{n}}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name:'Calculator',
  data(){
    return{
      calculatorValue:'',
      calculateorEle:['C','*','/','-','7','8','9','+','4','5','6','%','1','2','3','=','0','.'],
      operator:null,
      prval:''
    }
  },
  methods:{
    action(n){
      
      if(!isNaN(n) || n==='.'){
        this.calculatorValue +=n+''
      }
       
      if(n==='C'){
        this.calculatorValue=""
      }
      if(n==='%'){
        this.calculatorValue=this.calculatorValue/100 + ' ';
      }

      if(['/','*','-','+'].includes(n)){
        this.operator=n
        this.prval=this.calculatorValue;
        this.calculatorValue=""
      }

      if(n==='=' || ['/','*','-','+'].includes(n)){
        this.calculatorValue=eval(
          this.prval+this.operator+this.calculatorValue
        );
        this.prval=''
        this.operator=null
      }
    }
  }
}
</script>

<style scoped>
.bg-vu-dark{
  background-color: #31475e;
}
.hover-class:hover{
  cursor: pointer;
  background: #3d5875;
}
.bg-vue-green{
  background: #3fb984;
}
</style>