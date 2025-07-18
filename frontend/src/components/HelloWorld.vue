<template>
  <div>
    <button @click="fetchText">API 호출</button>
    <div v-if="result">{{ result }}</div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      result: ''
    };
  },
  methods: {
    async fetchText() {
      try {
        // 컨테이너 환경에서는 반드시 'http://backend:3000/'으로 호출
        const response = await axios.get('http://backend:3000/');
        this.result = response.data;
      } catch (error) {
        this.result = 'API 호출 에러: ' + error.message;
      }
    }
  }
};
</script>
