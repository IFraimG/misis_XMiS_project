<script setup lang="ts">
import { onMounted, ref, watchEffect, nextTick } from "vue"

import CustomHeader from "@/components/feature_main/CustomHeader.vue"
import MainInfo from "@/components/feature_main/MainInfo.vue"
import CustomFooter from "@/components/feature_main/CustomFooter.vue"
import ModalAuth from "@/components/feature_main/ModalAuth.vue"

const isAuth = ref<boolean | null>(false)


onMounted(async () => {
  nextTick(() => setTimeout(() => isAuth.value = true, 2000))

  // let result = await fetch("https://api.bankingapi.ru/extapi/aft/clientInfo/hackathon/v1/accounts", { method: "GET", headers: { Authorization: import.meta.env.VITE_API_ACCESS_TOKEN }  })
  // let resResult = await result.json()

  // console.log(resResult);
  
})

watchEffect(() => {
  if (isAuth.value) {
      document.body.style.overflow = "auto"
  } else document.body.style.overflow = "hidden"
})


const setAuth = (login: string) => {
  console.log(login);
  if (login.length == 0) {} else {
    // запрос
    isAuth.value = true
  }
}

</script>

<template>
  <div class="page__wrapper">
    <modal-auth @sendAuth="setAuth" v-if="!isAuth" />
    <div class="page">
      <div class="header__wrapper">
        <div class="header">
            <custom-header />
        </div>
      </div>
      <div class="main__wrapper">
        <div class="main">
          <main-info />
        </div>
      </div>
      <div class="footer__wrapper">
        <div class="footer">
          <custom-footer />
        </div>
      </div>
    </div>
  </div>
</template>
