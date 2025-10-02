<template>
  <div>
    <h2>예약 목록</h2>
    <!-- 총 예약 갯수 -->
    <p>총 예약 : {{ reservations.length }}건</p>
    <!-- 예약 추가 폼 -->
    <form class="form" @submit.prevent="addReservation">
      <input type="text" v-model="newName" placeholder="고객 이름" />
      <select v-model="newService">
        <option value="" disabled>서비스 선택</option>
        <option value="짐 보관">짐 보관</option>
        <option value="제빙기 청소">제빙기 청소</option>
      </select>
      <input type="date" v-model="newDate" />
      <button type="submit">예약 추가</button>
    </form>
    <!-- 예약 리스트 (예약건건이 다나와야해서 v-for)-->
    <div v-for="(item, index) in reservations" :key="index" class="card">
      <p>고객명 : {{ item.name }}</p>
      <p>서비스 : {{ item.service }}</p>
      <p>날짜 : {{ item.date }}</p>
      <!-- 예약 상태 -->
      <p v-if="item.done">✅ 완료</p>
      <p v-else>⏳ 대기중</p>
      <!-- 상태 바꾸기 버튼 -->
      <button @click="toggleStaus(index)">상태 바꾸기</button>
    </div>
  </div>
</template>
<script setup>
import { reactive, ref, watch, computed } from "vue";
const reservations = reactive([
  { name: "홍길동", service: "짐 보관", date: "2025-09-20", done: false },
  { name: "김철수", service: "제빙기 청소", date: "2025-10-01", done: false },
]);
// 새 예약 입력값(처음 초기값 빈배열)
const newName = ref("");
const newService = ref("");
const newDate = ref("");
// 예약 추가 함수
const addReservation = () => {
  // 입력창에 빈칸있으면 추가 안되게 경고창 띄우고 멈춰라(return=안하면 빈칸리스트 생성됨)
  if (!newName.value || !newService.value || !newDate.value) {
    alert("이름,서비스,날짜를 모두 입력하세요!");
    return;
  }
  // console.log("click");
  // reservations안에 넣어라
  reservations.push({ name: newName.value, service: newService.value, date: newDate.value, done: false });
  // 입력창 초기화
  newName.value = "";
  newService.value = "";
  newDate.value = "";
};
// 완료 / 대기 상태 토글(부정(!) 할당해서 변경되게 설정)
const toggleStaus = (index) => {
  // console.log(index);
  reservations[index].done = !reservations[index].done;
};
// 오늘 날짜 담기(오늘 이전 날짜 선택시 대기중이 되면 안됨!)
// const today = new Date()
// toISOString() 날째 객체를 국제표준시간 형식 문자열로 바꿔주는 함수
// split("T")[0] 잘라내겠다 T부터
const today = new Date().toISOString().split("T")[0];
// console.log(today);     //2025-09-29T02:17:09.911Z  국제표준시간 출력형태
// 날짜가 지났으면 자동 완료 처리
// watch() 날짜 변경 감시
watch(
  reservations,
  (newVal) => {
    newVal.forEach((item) => {
      if (item.date < today) {
        item.done = true; //날짜가 오늘보다 이전이면 완료 처리
      }
    });
  },
  // watch에서 설정 변경하는것
  //  deep:깊게 감시(예약 배열안에 있는 item.done같은 속성도 감시해라)
  // immediate : 화면 열리자마자 지난 날짜는 바로 완료 처리
  { deep: true, immediate: true }
);
// 예약 총 갯수
const totalReservations = computed(()=>{
  return reservations.length
});
</script>
<style scoped></style>
