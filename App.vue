<template>

<!-- <div class="start" :class="{end : 모달창열렸니}">
<Modal @closeModal="모달창열렸니 = false" :원룸들 = "원룸들" 
:누른거="누른거" :모달창열렸니="모달창열렸니" />
</div> -->
<transition name="fade">
<Modal @closeModal="모달창열렸니 = false" :원룸들 = "원룸들" 
:누른거="누른거" :모달창열렸니="모달창열렸니" />
</transition>


  <div class="menu">
    <a v-for="작명 in menu" :key="작명"> {{작명}} </a>
  </div>

<Discount/>

<button @click="priceSort">가격순정렬</button>
<button @click="alphabetic">가나다순정렬</button>
<button @click="sortBack">되돌리기</button>
 
  <!-- <div v-for="(a,i) in products" :key="i">
    <h4>{{a}} </h4>
      <p>50만원</p>
  </div> -->
  <!-- <div>
    <img src="./assets/room0.jpg" class="room-img">
    <h4 @click="모달창열렸니 = true">{{products[0]}} </h4>
      <p>50만원</p>
      <button @click="increase1">허위매물신고</button> <span> 신고수1: {{신고수1}} </span>
  </div>
  <div>
    <img src="./assets/room1.jpg" class="room-img">
    <h4>{{products[1]}} </h4>
      <p>60만원</p>
      <button @click="increase2">허위매물신고</button> <span> 신고수2: {{신고수2}} </span>
  </div>
  <div>
    <img src="./assets/room2.jpg" class="room-img">
    <h4>{{products[2]}} </h4>
      <p>70만원</p>
      <button @click="increase3">허위매물신고</button> <span> 신고수3: {{신고수3}} </span>
  </div> -->

  <!-- <div v-for="(a,i) in 원룸들" :key="i">
    <img :src="원룸들[i].image" class="room-img">
     <h4 @click="모달창열렸니= true; 누른거 = i ">{{원룸들[i].title}}</h4> 
      <p>{{원룸들[i].price}}원</p>      
  </div> -->

<Cards @openModal="모달창열렸니 = true; 누른거 = $event" :원룸="원룸들[i]" 
v-for="(작명,i) in 원룸들" :key="작명" /> 
<!-- <Cards :원룸="원룸들[1]"/>
<Cards :원룸="원룸들[2]"/>
<Cards :원룸="원룸들[3]"/>
<Cards :원룸="원룸들[4]"/>
<Cards :원룸="원룸들[5]"/>
  -->


</template>

<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Cards from './Cards.vue';

export default {
  name: 'App',
  data(){
    return{      
      원룸들오리지널 : [...data],
      누른거 : 0,
      원룸들 : data,
      모달창열렸니: false,
      신고수1 : 0,
      신고수2 : 0,
      신고수3 : 0,
      menu :['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸']
    }
  },

  methods :{
    increase1(){
      this.신고수1 += 1;      
    },
    increase2(){
      this.신고수2 += 1;      
    },
    increase3(){
       this.신고수3 += 1;      
    },
    priceSort(){
      this.원룸들.sort(function(a,b){
        return a.price - b.price;
      })      
    },
    sortBack(){
      this.원룸들 = [...this.원룸들오리지널];
    },
    alphabetic(){
      let rooms = [...this.원룸들.title]
      rooms.sort();
            
    }
  },

  components: {
    Discount : Discount,
    Modal : Modal,
    Cards : Cards,
  }
}
</script>

<style>
/* .start{
  opacity: 0;
  transition: all 1s;
}
.end{
  opacity :1;
} */
.fade-enter-from{
  transform: translateY(-1000px);
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
  transform: translateY(0px);
}

.fade-leave-from{
  opacity: 1;
}
.fade-leave-active{
  transition: all 1s;
}
.fade-leave-to{
  opacity: 0;
}
body {
  margin : 0
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; 
  padding: 20px;
}
.white-bg{
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img{
  width: 100%;
  margin-top: 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}
.menu {
  background: darkslateblue;
  padding:15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding:10px;
}

.discount {
  background: #eee;
  padding: 10px;
  margin:10px;
  border-radius: 5px;
}
</style>
