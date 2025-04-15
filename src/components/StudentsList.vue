<script setup>
    import {ref,inject } from 'vue';
    const CurrentScreen=inject('CurrentScreenAll');
    const infor=inject('inforall');
    const Xoahocsinh=(index,index1,index2)=>{
        infor.value[index].lops[index1].students.splice(index2,1);
    }
    const themhocsinh=()=>{
        CurrentScreen.value='themhocsinh';
    };
    const SUA=(index,index1,index2)=>{
        const student = infor.value[index].lops[index1].students[index2];
        student.name = prompt("Nhập lại tên học sinh:", student.name);
        student.age = prompt("Nhập lại tuổi học sinh:", student.age); 
    }
    const dslop=()=>{
        CurrentScreen.value='dslop';
    }

</script>
<template v-if="CurrentScreen.value==='dsachhocsinh'">
    <button @click="themhocsinh">Thêm Học Sinh</button>
    <table border="1">
        <thead>
            <tr>
                <th>STT</th>
                <th>Họ Và Tên</th>
                <th>Tuổi</th>
                <th>Lớp</th>
                <th>Thao Tác</th>
            </tr>
        </thead>
        <tbody>
            <template v-for="(nganh,index) in infor" :key="index">
                <template v-for="(caclop,index1) in nganh.lops" :key="index1">
                    <tr v-for="(student,index2) in caclop.students" :key="index2">
                        <td>{{ (index+1)+'.'+(index1+1)+'.'+(index2+1) }}</td>
                        <td>{{ student.name }}</td>
                        <td>{{ student.age }}</td>
                        <td>{{ caclop.lop }}</td>
                        <td>
                            <button @click="SUA(index,index1,index2)">SỬA</button>
                            <button @click="Xoahocsinh(index,index1,index2)">XÓA</button>
                        </td>
                    </tr>
                </template>
            </template> 
        </tbody>
    </table>
    <button @click="dslop">Chuyển sang danh sách lớp</button>
</template>