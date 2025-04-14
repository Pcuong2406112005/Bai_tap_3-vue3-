<script setup>
  import {ref} from 'vue';
  import StudentsList from './components/StudentsList.vue';
  const infor =ref([
    {
      nganh:'CNTT',
      lops:[
        {lop:'CN01',students:[{name:'Phan Mạnh Cường',age:20}]}
      ]
    },
    {
      nganh:'CNDPT',
      lops:[
        {lop:'PT01',students:[{name:'Lê Quốc Dũng',age:20}]}
      ]
    }
  ])
  let currentIndex=1;
</script>
<template>
  <table border="1">
    <thead>
      <tr>
        <th>STT</th>
        <th>Họ Và Tên</th>
        <th>Lớp</th>
        <th>Thao Tác/Xóa</th>
      </tr>
    </thead>
    <tbody>
      <template v-for="(nganh, index) in infor" :key="index">
        <template v-for="(lop, index1) in nganh.lops" :key="index1">
          <StudentsList :lopName="lop.lop" :students="lop.students" :nganhindex="index" :lopindex="index1"/>
        </template>  
      </template>
    </tbody>
  </table>
</template>