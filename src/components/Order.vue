<template>
  <div class="order">
    <div class="inputRegion">
      <div :class="i.class" v-for="i in info">
        <span>{{ i.description }}: </span
        ><input :type="i.type" v-model="i.content" />
      </div>

      <button @click="pushInList">新增項目</button>
    </div>
    <div class="prodList" v-show="list.length > 0">
      <div class="items" v-for="j in list" :key="j.key">
        <div class="round att">🔴</div>
        <div class="name att">{{ j.name }}</div>
        <div class="number att">x{{ j.num }}</div>
        <div class="price att">${{ j.price }}</div>
        <div class="member att">{{ j.member }}</div>
        <div class="note att">{{ j.note }}</div>
        <div class="delete" @click="delItem(j)">×</div>
      </div>
    </div>

    <div class="result" v-show="total">
      <div class="totalPrice">總共 {{ total }} 元</div>
    </div>
  </div>

  <div class="analysis">
    <div class="conclusion">
      <button
        class="createPopList"
        @click="showPopList"
        v-show="list.length > 0"
      >
        產生統計
      </button>
      <div class="resultList" v-show="popList">
        <h2>餐點明細</h2>
        <div class="close" @click="showPopList">×</div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup name="Order">
import { ref } from "vue";

let list = ref([]);

alert("修改功能還未實現");

let info = [
  {
    description: "品項",
    type: "text",
    class: "item",
    content: "焙香決明大麥",
  },
  {
    description: "數量",
    type: "number",
    class: "number",
    content: "1",
  },
  {
    description: "單價",
    type: "number",
    class: "price",
    content: "40",
  },
  {
    description: "人員",
    type: "text",
    class: "member",
    content: "Joe",
  },
  {
    description: "備註",
    type: "text",
    class: "note",
    content: "去冰/無糖/加珍珠",
  },
];

// 提交使用
function pushInList() {
  // 先判定內容是否完整

  for (let i = 0; i < info.length - 1; i++) {
    if (info[i].content == "") {
      alert("您的 [" + info[i].description + "] 沒有填寫完整");
      return;
    }
  }

  let item = {
    name: info[0].content,
    num: Number(info[1].content),
    price: Number(info[2].content),
    member: info[3].content,
    note: info[4].content,
    key: Date.now(),
  };

  list.value.push(item);

  // console.log(item);
  console.log(list.value);

  setTotal();
}

function delItem(j) {
  // console.log(j.key);
  const objStamp = j.key;

  for (let i = 0; i < list.value.length; i++) {
    // console.log(list.value[i].key);
    // console.log(objStamp);

    if (list.value[i].key == objStamp) {
      console.log("🔺您刪除了品項: " + list.value[i].name);
      list.value.splice(i, 1);

      setTotal();
      return;
    }
  }
}

let total = ref(0);

function setTotal() {
  // console.log("程式有被執行");
  // console.log(list.value.length);

  let sum = 0;
  for (let k = 0; k < list.value.length; k++) {
    sum += list.value[k].num * list.value[k].price;
  }
  total.value = sum;
}

let popList = ref(false);

function showPopList() {
  popList.value = !popList.value;
}
</script>

<style scoped>
.order {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.inputRegion {
  margin-top: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 5px;
}

* {
  /* border: 1px solid gray; */
  box-sizing: border-box;
}

.prodList {
  padding: 30px;
  margin-top: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: 2px solid #99c199;
  text-align: center;
  width: 80%;
  flex-direction: column;
  /* background-color: rgb(247, 247, 247); */
}

.items {
  display: flex;
  font-display: row;
  padding: 10px;
  background-color: rgba(180, 229, 180, 0.2);
  border-right: 2px solid #799a79;
  border-bottom: 2px solid #799a79;
  margin-top: 5px;
  box-shadow: 0px 0px 1rem rgba(180, 229, 180, 1);
  border-radius: 5px;
  width: 90%;
  position: relative;
  transition: 0.5s;
  user-select: text;
  letter-spacing: 1px;
}
.items:hover {
  background-color: rgba(180, 229, 180, 0.6);
}

.att {
  display: flex;
  justify-content: center;
  align-items: center;
}

.items .name {
  background-color: #fff;
  padding: 5px;
  border-radius: 7px;
  font-weight: 700;
  height: 2rem;
  width: 15rem;
  font-size: 1.2rem;
}

.items .member {
  font-weight: 800;
  padding: 5px;
  border-radius: 7px;
  /* background-color: #93defa; */
  background-color: #fce38b;
}

.items .note {
  color: #40524089;
  text-align: left;
}

.items .delete {
  margin-left: 70px;
  font-size: 1.3rem;
  font-weight: 900;
  color: #405240;
  cursor: pointer;
  position: absolute;
  right: 20px;
  user-select: none;
}

.items .delete:active {
  transform: scale(0.8);
}

.items .att {
  margin: 0 20px 0 0;
}

.result {
  /* border: 1px solid #000; */
  margin: 15px 0 50px 0;
  color: red;
  font-size: 2rem;
  font-weight: 700;
  position: relative;
  left: 30vw;
}

.resultList {
  background-color: white;
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 600px;
  height: 700px;
  display: flex;
  flex-direction: column;
  border-radius: 10px;
  border: 5px solid #799a79;
  /* display: none; */
}

.resultList h2 {
  letter-spacing: 2px;
  text-align: center;
  padding: 20px;
  font-size: 2rem;
  color: #374637;
}

.resultList .close {
  position: absolute;
  font-size: 2rem;
  right: 3%;
  top: 3%;
  font-weight: 900;
  color: #374637;
}

.analysis {
  display: flex;
  justify-content: center;
}

@media (max-width: 768px) {
  .prodList {
    width: 100%;
  }
  .items {
    width: 100%;
  }
  .items .name {
    width: auto;
  }
  .items .round {
    display: none;
  }
}
</style>
@/hooks/popList
