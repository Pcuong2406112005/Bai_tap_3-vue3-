<script setup>
    import {inject,ref} from 'vue';
    const infor=inject('inforall');
    const CurrentScreen=inject('CurrentScreenAll');
    const dshocsinh=()=>{
        CurrentScreen.value='dsachhocsinh';
    }
    const Xoalop=(index,index1)=>{
        infor.value[index].lops.splice(index1,1);
    }
    const Xoanganh=(index)=>{
        infor.value.splice(index,1);
    }
    const Suanganh = (index) => {
        const nganh = infor.value[index];
        const tenMoi = prompt('Nhập tên ngành mới', nganh.nganh);
        if (tenMoi !== null && tenMoi.trim() !== '') {
            nganh.nganh = tenMoi;
        }
    };
    const Sualop = (index,index1) => {
        const lop = infor.value[index].lops[index1];
        const tenMoi = prompt('Nhập tên lớp mới', lop.lop);
        if (tenMoi !== null && tenMoi.trim() !== '') {
            lop.lop = tenMoi;
        }
    };
    const themlop=()=>{
        CurrentScreen.value='themlop';
    }
</script>
<template v-if="CurrentScreen.value==='dslop'">
    <button @click="themlop">Thêm Lớp</button>
    <table border="1">
        <thead>
            <tr>
                <th>STT</th>
                <th>Lớp</th>
                <th>Thao Tác</th>
            </tr>
        </thead>
        <tbody>
            <template v-for="(nganh_,index) in infor" :key="index">
                <tr>
                    <td>{{ index+1 }}</td>
                    <td>{{ nganh_.nganh }}</td>
                    <td>
                        <button @click="Suanganh(index)">Sửa Ngành</button>
                        <button @click="Xoanganh(index)">Xóa Ngành</button>
                    </td>
                </tr>
                <tr v-for="(LOP,index1) in nganh_.lops" :key="index1">
                    <td>{{ (index+1)+'.'+(index1+1) }}</td>
                    <td>{{ LOP.lop }}</td>
                    <td>
                        <button @click="Sualop(index,index1)">Sửa Lớp</button>
                        <button @click="Xoalop(index,index1)">Xóa Lớp</button>
                    </td>
                </tr> 
            </template>
        </tbody>
    </table>
    <button @click="dshocsinh">Quay về danh sách học sinh</button>
</template>