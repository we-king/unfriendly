<script setup>
import users from '@/stores/users'
import { ref, watch } from 'vue'
import { isEmptyString } from '@/utils'

let value = ref("")
let rlt = ref([])

watch(value, (nValue) => {
  if (isEmptyString(nValue)) {
    rlt.value = [];
    return;
  }
  let black = users.filter((user) => {
    return user.indexOf(nValue) >= 0;
  })
  rlt.value = black
})

</script>

<template>
  <div>
    <div class="title"><span>黑名单查询</span></div>
    <div>
      <input title="search user" placeholder="请输入账号" type="text" v-model="value">
    </div>
    <div v-if="rlt.length > 0">
      <li v-for="(user, idx) in rlt" :key="idx">
        {{ user }}
      </li>
    </div>
    <div v-else class="empty">
      无结果
    </div>
  </div>
</template>

<style scoped>
.title {
  text-align: center;
}
.empty {
  text-align: center;
}
</style>