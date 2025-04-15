<script setup>
  import { ref, provide, watch } from 'vue';
  import StudentsList from './components/StudentsList.vue';
  import AddStudent from './components/AddStudents.vue';
  import ClassList from './components/ClassList.vue'
  import AddClass from './components/AddClass.vue';
  const infor = ref([
    { nganh: 'CNTT', lops: [{ lop: 'CN01', students: [{ name: 'Phan Mạnh Cường', age: 20 }] }] },
    { nganh: 'CNDPT', lops: [{ lop: 'PT01', students: [{ name: 'Lê Quốc Dũng', age: 20 }] }] }
  ]);
  if (localStorage.getItem('inforData')) {
    infor.value = JSON.parse(localStorage.getItem('inforData'));
  }
  provide('inforall', infor);
  const currentscreen = ref('dsachhocsinh');
  provide('CurrentScreenAll', currentscreen);
  const keyword = ref('');
  watch(infor, (newValue) => {
    localStorage.setItem('inforData', JSON.stringify(newValue));
  });
</script>
<template>
  <StudentsList v-if="currentscreen === 'dsachhocsinh'"></StudentsList>
  <AddStudent v-if="currentscreen === 'themhocsinh'"></AddStudent>
  <ClassList v-if="currentscreen==='dslop'"></ClassList>
  <AddClass v-if="currentscreen==='themlop'"></AddClass>
  <template v-if="currentscreen==='dsachhocsinh'">
    <input v-model="keyword" placeholder="Tìm học sinh" />
    <table border="1" v-if="keyword">
      <thead>
        <tr><th>STT</th><th>Họ tên</th><th>Tuổi</th><th>Lớp</th><th>Ngành</th></tr>
      </thead>
      <tbody>
        <tr v-for="(nganh, nganhIndex) in infor" :key="nganhIndex">
          <tr v-for="(lop, lopIndex) in nganh.lops" :key="lopIndex">
            <tr v-for="(student, studentIndex) in lop.students" :key="studentIndex" v-if="student.name.toLowerCase().includes(keyword.toLowerCase())">
              <td>{{ nganhIndex+1 }}.{{ lopIndex+1 }}.{{ studentIndex+1 }}</td>
              <td>{{ student.name }}</td><td>{{ student.age }}</td><td>{{ lop.lop }}</td><td>{{ nganh.nganh }}</td>
            </tr>
          </tr>
        </tr>
      </tbody>
    </table>
  </template>
</template>
