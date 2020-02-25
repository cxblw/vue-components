# cx-vue-components

### 大屏数字滚动

```vue
<template>
  <div>
    <div class="box">
      <p class="box-item" v-for="(item,index) in orderNum" :key="index">
        <span ref="numberItem">0123456789</span>
      </p>
      
    </div>
  </div>
</template>


<script>
export default {
    props:{
        num:{
            type:[String, Number],
            required: true
        }
    },
    data() {
        return {
            orderNum:['0','0','0','0']
        }
    },
    mounted() {        
        let timer
        let _that = this
        clearInterval(timer)
        timer = setInterval(() => { 
            let numberArr 
            if (typeof(this.num) == 'string') {
                numberArr = this.num
            }else if(typeof(this.num) == 'number'){
                numberArr = this.num.toString()
            }
            _that.toOrderNum(numberArr)
        }, 1000);
    },
    methods: {
        setNumberTransform() {           
            let numberItems = this.$refs.numberItem            
            for (let index = 0; index < this.orderNum.length; index++) {
                console.log()
                let elem = numberItems[index];
                elem.style.transform = `translate(-50%, -${this.orderNum[index] * 10}%)`;
            }
             
        },
        toOrderNum(num) {                   
            if (num.length < 4) {
                num = '0' + num // 如未满八位数，添加"0"补位                
                this.toOrderNum(num) // 递归添加"0"补位
            } else if (num.length === 4) {                               
                this.orderNum = num.split('') // 将其便变成数据，渲染至滚动数组
                this.setNumberTransform()
            } 
        },
        
    },
}
</script>


<style  scoped>
.box-item {
  display: inline-block;
  width: 47px;
  height: 60px;
  margin-left:12px;
  background: url(../assets/images/icon_num.png) no-repeat center center;
  background-size: 100% 100%;
  font-size: 62px;
  line-height: 82px;
  text-align: center;
  position: relative;
  writing-mode: vertical-lr;
  text-orientation: upright;
  user-select:none;
  overflow: hidden;
}
.box-item span {
  transition: 0.5s all ease-in;
  position: absolute;
  color:#fff;
  top: -5px;
  left: 50%;
  transform: translate(-50%,0%);
  letter-spacing: 10px;
}

</style>
```

