<template>
  <div class="product-detail">
    <h2>🛒상품 상세보기</h2>
    <!-- 탭 버튼 -->
    <div class="tab-menu">
      <button @click="activeTab = 'information'">📖상품 정보</button>
      <button @click="activeTab = 'review'">⭐리뷰</button>
      <button @click="activeTab = 'delivery'">🚚배송 /환불</button>
    </div>
    <!-- 탭 내용 -->
    <div v-if="activeTab === 'information'">
      <h3>상품정보</h3>
      <p>이 상품은 100% 천연 원료로 만들어젔습니다.</p>
    </div>
    <div v-if="activeTab === 'review'">
      <h3>⭐ 리뷰</h3>
      <ul>
        <li>홍길동 : 정말 좋아요 👍</li>
        <li>김철수 : 배송 빨라요 🚀</li>
      </ul>
    </div>
    <div v-if="activeTab === 'delivery'">
      <h3>🚚 배송/환불</h3>
      <p>배송: 2~3일 소요 ⏱</p>
      <p>환불: 상품 수령 후 7일 이내 가능 ✅</p>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";

const activeTab = ref("information");
</script>
<style scoped>
.product-detail {
  max-width: 500px;
  margin: auto;
  font-family: Arial, sans-serif;
}
.tab-menu {
  margin-bottom: 10px;
}
button {
  margin: 5px;
  padding: 8px 14px;
  border: 1px solid #333;
  background: #f5f5f5;
  cursor: pointer;
}
button:hover {
  background: #ddd;
}
</style>
