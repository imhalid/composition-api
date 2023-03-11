<script>
import { computed, ref, watch, watchEffect } from 'vue'
export default {
  setup() {
    const count = ref(0)
    const type = ref('')
    const isType = ref(false)
    const oddOrEven = computed(() => (count.value % 2 === 0 ? 'even' : 'odd'))
    const hello = ref('Hello World')
    const show = ref(false)
    const toggle = () => {
      show.value = !show.value
    }

    const counter = () => {
      count.value++
    }

    watch(count, (newValue, oldValue) => {
      console.log('count changed', newValue, oldValue)
    })

    watchEffect(stop => {
      type.value.length > 0 ? (isType.value = true) : (isType.value = false)

      const time = setInterval(() => {
        isType.value = false
      }, 1000)

      stop(() => {
        clearInterval(time)
      })
    })

    return { hello, show, toggle, count, counter, oddOrEven, type, isType }
  },
}
</script>

<template>
  <div class="flex flex-col space-y-5">
    <button @click="counter">+ {{ count }} {{ oddOrEven }}</button>
    <div class="flex">
      <input type="text" v-model="hello" />
      <p class="ml-5">{{ hello }}</p>
    </div>
    <div class="flex">
      <input type="text" v-model="type" />
      <p v-if="isType" class="ml-5">typing...</p>
    </div>
    <button @click="toggle">Toggle</button>
    <p v-if="show" :style="show && 'color: green;'" class="w-72 text-start">
      Lorem ipsum, dolor sit amet consectetur adipisicing elit. Quod odit
      ratione culpa nisi, doloribus porro animi qui necessitatibus ut sapiente,
      distinctio ipsam molestias corrupti iste corporis optio suscipit illum
      quo!
    </p>
  </div>
</template>
