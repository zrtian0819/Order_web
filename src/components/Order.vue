<template>
  <div class="order">
    <div class="inputRegion">
      <div :class="i.class" v-for="i in info">
        <span>{{ i.description }}: </span
        ><input :type="i.type" v-model="i.content" />
      </div>

      <button @click="pushInList">確定</button>
    </div>
    <div class="prodList" v-show="list.length > 0">
      <div class="items" v-for="j in list" :key="j.key">
        <div class="round att">🔴</div>
        <div class="name att">{{ j.name }}</div>
        <div class="number att">x{{ j.num }}</div>
        <div class="price att">${{ j.price }}</div>
        <div class="note att">{{ j.note }}</div>
        <div class="delete" @click="delItem(j)">×</div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup name="Order">
import { ref } from "vue";
let list = ref([]);

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
    description: "備註",
    type: "text",
    class: "note",
    content: "去冰無糖加珍珠",
  },
];

// 提交使用
function pushInList() {
  // 先判定內容是否完整

  for (let i = 0; i < info.length; i++) {
    if (info[i].content == "") {
      alert("[" + info[i].description + "] 沒有填寫完整");
      return;
    }
  }

  let item = {
    name: info[0].content,
    num: info[1].content,
    price: info[2].content,
    note: info[3].content,
    key: Date.now(),
  };

  list.value.push(item);

  console.log(item);
}

function delItem(j) {
  // console.log(j.key);
  const objStamp = j.key;

  for (let i = 0; i < list.value.length; i++) {
    // console.log(list.value[i].key);
    // console.log(objStamp);

    if (list.value[i].key == objStamp) {
      console.log("🔺刪除了品項: " + list.value[i].name);
      list.value.splice(i, 1);
      return;
    }
  }
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
  /* border: 1px solid #000; */
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
  width: 80vw;
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
  box-shadow: 0px 0px 1rem rgba(180, 229, 180, 0.5);
  /* border-radius: 5px; */
  width: 90%;
  position: relative;
  transition: 0.3s;
  user-select: text;
}
.items:hover {
  transform: scale(1.01);
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
