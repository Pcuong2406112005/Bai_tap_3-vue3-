<script setup>
    defineProps({
        lopName: String,
        students: Array,
        nganhindex: Number,
        lopindex:Number,
    });
</script>
<template>
<template v-for="(student,index) in students" :key="index">
     <tr>
        <td>{{ (nganhindex+1)+'.'+(lopindex+1)+'.'+(index+1) }}</td>
        <td>{{ student.name }}</td>
        <td>{{ lopName }}</td>
        <td></td>
    </tr>
</template>
</template>