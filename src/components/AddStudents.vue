<script setup>
    import {inject,watch,ref} from 'vue';
    const CurrentScreen=inject('CurrentScreenAll');
    const infor=inject(('inforall'));
    const Luu=()=>{
        if(student.value.HoTen!==''&&student.value.Tuoi!==null&&index_1.value!==null&&index_2.value!==null){
            infor.value[index_1.value].lops[index_2.value].students.push({
                name:student.value.HoTen,
                age:student.value.Tuoi,
            });
            student.value.HoTen='';
            student.value.Tuoi=null;
            index_1.value=null;
            index_2.value=null;
            lop.value=null;
            CurrentScreen.value='dsachhocsinh';
        }
        else{
            alert('Hãy nhập đủ thông tin');
        }
    }
    const student=ref({
        HoTen:'',
        Tuoi:null,
    })
    const index_1=ref(null);
    const index_2=ref(null);
    const chon=(value)=>{
        const {nganhIndex,lopIndex}=value;
        index_1.value=nganhIndex;
        index_2.value=lopIndex;
    }
    const lop=ref(null);
</script>
<template v-if="CurrentScreen.value==='themhocsinh'">
    Họ và Tên:<input v-model="student.HoTen"><br>
    Tuổi:<input v-model="student.Tuoi"><br>
    <select v-model="lop" @change="chon(lop)">
        <option disabled value="">--Chọn Lớp--</option>
        <template v-for="(nganh_,index) in infor" :key="index">
            <option disabled>{{ nganh_.nganh }}</option>
            <template v-for="(caclop,index1) in nganh_.lops" :key="index1">
                <option :value="{nganhIndex:index,lopIndex:index1}">{{ caclop.lop }}</option>
            </template>
        </template>
    </select>    
    <button @click="Luu">Lưu</button>
</template>