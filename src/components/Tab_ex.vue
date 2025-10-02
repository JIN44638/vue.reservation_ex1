<template>
  <div class="tab-box">
    <h2>탭 메뉴 예제</h2>
    <!-- 탭 버튼 -->
    <button @click="activeTab = 'home'">🏠홈</button>
    <button @click="activeTab = 'about'">ℹ️소개</button>
    <button @click="activeTab = 'contact'">📞연락</button>
    <!-- 탭 내용 -->
    <div v-if="activeTab === 'home'">
      <h3>🏠홈 화면</h3>
      <p>여기는 메인 페이지입니다.</p>
    </div>
    <div v-if="activeTab === 'about'">
      <h3>ℹ️소개 화면</h3>
      <p>여기는 Tab 기능 연습 페이지입니다.</p>
    </div>
    <div v-if="activeTab === 'contact'">
      <h3>📞연락 화면</h3>
      <p>문의 : gmail@gmail.com</p>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";

// 현재 어떤 탭을 눌렀는지 저장(첫화면을 "home"으로 )
const activeTab = ref("home");
</script>

<style scoped>
.tab-box {
  max-width: 400px;
  margin: auto;
  text-align: center;
}
button {
  margin: 5px;
  padding: 8px 12px;
  border: 1px solid #333;
  background: #eee;
  cursor: pointer;
}
button:hover {
  background: #ddd;
}
</style>
