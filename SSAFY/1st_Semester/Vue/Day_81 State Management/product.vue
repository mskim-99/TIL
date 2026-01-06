import { ref, computed } from 'vue'
import { defineStore } from 'pinia'

export const useProductStore = defineStore('product', () => {
  const products = ref([])

  // 외부에서 axios로 json 데이터 불러오기
  // get() 내부에 문자열 형태로 url 작성
  const fetchProducts = async () => {
    const res = await axios.get('https://jsonplaceholder.typicode.com/posts')
    products.value = res.data
  }

  

  return { products, fetchProducts }
})
