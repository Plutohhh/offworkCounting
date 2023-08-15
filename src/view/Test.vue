<template>
  <div class="container">
    <div class="grid-container">
      <div class="item item-1">1</div>
      <div class="item item-2">2</div>
      <div class="item item-3">3</div>
      <div class="item item-4">4</div>
      <div class="item item-5">5</div>
      <div class="item item-6">6</div>
      <div class="item item-7">7</div>
      <div class="item item-8">8</div>
      <div class="item item-9">9</div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

let set1 = new Set([6,8,7,0]);
let set2 = new Set([1,2,3]);
let difference = new Set([...set1].filter(x => !set2.has(x)))
console.log(difference);
let map = new Map();
map.set('1','123')
map.set('1','456')
console.log(map);

// for(let item of set.entries()){
//   console.log(item);
// }


</script>

<style scoped lang="scss">
.container {
  height: 100%;
  width: 100%;
  // background-color: rgb(209, 209, 209);
  display: flex;
  justify-content: center;
  align-items: center;
  .grid-container
  {
    width: 30%;
    height: 50%;
    border: 1px solid rgb(116, 214, 146);
    display: grid;
    // grid-template-rows:  80px 90px;
    grid-template-columns: 1fr 2fr;
    gap: 10px 20px;
    // align-content: space-around;
    // grid-template-rows: repeat(2, 1fr 5fr);
    // grid-row-gap: 1fr;
    // column-gap: 20px;
    // row-gap: 20px;


    .item {
      font-size: 2em;
      text-align: center;
      border: 1px solid #e5e4e9;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .item-1 {
      background-color: #ef342a;
    }

    .item-2 {
      background-color: #f68f26;
    }

    .item-3 {
      background-color: #4ba946;
    }

    .item-4 {
      background-color: #0376c2;
    }

    .item-5 {
      background-color: #c077af;
    }

    .item-6 {
      background-color: #f8d29d;
    }

    .item-7 {
      background-color: #b5a87f;
    }

    .item-8 {
      background-color: #d0e4a9;
    }

    .item-9 {
      background-color: #4dc7ec;
    }
  }
}
</style>
