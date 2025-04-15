<script setup>
import { inject, ref } from 'vue';
const infor = inject('inforall');
const CurrentScreen = inject('CurrentScreenAll');
const lopName = ref('');
const NganhIndex = ref(null);
const saveClass = () => {
  if (lopName.value && NganhIndex.value !== null) {
    infor.value[NganhIndex.value].lops.push({ lop: lopName.value });
    lopName.value = '';
    NganhIndex.value = null;
    CurrentScreen.value = 'dslop';
  } else {
    alert('Hãy đầy đủ thông tin!');
  }
};
</script>

<template v-if="CurrentScreen.value === 'themlop'">
  <div>
    <label for="lopName">Tên lớp:</label>
    <input id="lopName" v-model="lopName" placeholder="Nhập tên lớp" />
  </div>
  <div>
    <label for="nganh">Chọn ngành:</label>
    <select id="nganh" v-model="NganhIndex">
      <option disabled value="">-- Chọn ngành --</option>
      <template v-for="(nganh, index) in infor" :key="index">
        <option :value="index">{{ nganh.nganh }}</option>
      </template>
    </select>
  </div>
  <div>
    <button @click="saveClass">Lưu</button>
  </div>
</template>
