<template>
  <div class="container">
    <h1>promise</h1>
    <div></div>
    <div class="fater">
      <div class="son">
      </div>
      <div class="text">
          随着人工智能技术的快速发展，自然语言处理领域的研究取得了巨大的进展。ChatGPT，即Chat(聊天) Generative Pre-trained Transformer(生成式预训练转换器)，是OpenAI公司最新发布的尖端模型。它采用了预训练和微调的两个步骤，能够根据输入的问题产生相关且连贯的回答，实现智能聊天的功能。
          随着人工智能技术的快速发展，自然语言处理领域的研究取得了巨大的进展。ChatGPT，即Chat(聊天) Generative Pre-trained Transformer(生成式预训练转换器)，是OpenAI公司最新发布的尖端模型。它采用了预训练和微调的两个步骤，能够根据输入的问题产生相关且连贯的回答，实现智能聊天的功能。
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// var aaa = {
//   aaa: '111',
// }
// let b = {
//   aaa: '222',
//   a: () => {
//     console.log(this.aaa)
//     console.log(this)
//   },
// }
// b.a()
// const promise2 = promise1.then(() => {
//   throw new Error('error!!!')
// })
const p1 = Promise.resolve(1)
const p2 = Promise.reject(2)
// try {
//   Promise.reject(3)
// } catch (err) {
//   console.log('=====================\n')
//   console.log(err)
// }

// Promise.all([p1, p1, p2])
//   .then(res => {
//     console.log('succ');
//     console.log(res)
//   })
//   .catch(err => {
//     console.log('err');
    
//     console.log(err)
//   })

const res = async () => {
  const res = await Promise.allSettled([p1, p2])
  // const res = await Promise.resolve(1)
  return res
}
async function onPromise() {
  // const res = await Promise.allSettled([p1, p2])
  let res
  try {
    res = await Promise.reject(3)
  } catch (err) {
    console.log('=====================\n')
    console.log(err)
  }
  console.log('res=====================\n', res)
  return res
}

// onPromise()

// async 中的promise reject了，不会报错？

// setTimeout(() => {
//   console.log(p1)
//   console.log(p2)
//   console.log(promise1)
//   console.log(promise2)
// }, 10)
</script>

<style scoped lang="scss">
.container {
  height: 100%;
  width: 100%;
  padding: 0 30px 0;
  text-align: left;
  // color: #3c2147;
  overflow-y: auto;
  overflow-x: hidden;
  .fater {
    border: 1px solid red;
    width: 20%;
    height: 20%;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    .son {
      float: left;
      width: 150px;
      height: 150px;
      background-color: red;
    }
    // .fater::after
    // {
    //   content:"";
    //   clear: both;
    //   display: block;
    // }
    // .son::after{
    //   content: ""; /* 内容设置为空*/
    //   display: block; /* 设置为块级元素*/
    //   clear: both; /* 清除浮动*/
    // }
  }
  .fater::after
  {
    content:"";
    clear: both;
    display: block;
  }
}
</style>
