<script setup>
import { ref, watch } from 'vue'
import { isEmptyString } from '@/utils'
import axios from "axios"


let value = ref("")
let rlt = ref([])
let users = ref([])

axios.get("./blacks.json").then(({ data }) => {
  users.value = data
}).catch(() => {
  users.value = []
})

watch(value, (nValue) => {
  if (isEmptyString(nValue)) {
    rlt.value = [];
    return;
  }
  let black = users.value.filter((user) => {
    return user.indexOf(nValue) >= 0;
  })
  rlt.value = black
})

</script>

<template>
  <div>
    <div class="center"><span>黑名单查询</span></div>
    <div class="center">
      <input title="search user" placeholder="请输入账号" type="text" v-model="value">
    </div>
    <div v-if="rlt.length > 0">
      <li v-for="(user, idx) in rlt" :key="idx">
        {{ user }}
      </li>
    </div>
    <div v-else class="center">
      无结果
    </div>
  </div>
</template>

<style scoped>
.center {
  text-align: center;
}
</style>