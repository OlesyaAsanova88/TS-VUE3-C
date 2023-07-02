<script setup lang="ts">
import { GENDER, type Invitee } from '@/taype';
//import { defineProps } from "vue"//? не понимаю почему импорт не нужен

//const props = defineProps(['invitee'])
// enum GENDER {
//   MALE,
//   FEMALE
// }

defineProps<{
    invitee: Invitee
//     invitee: {
//     id: number;
//     name: string;
//     gender: GENDER
//   }
}>()
</script>

<template>
    <div
    :style="{backgroundColor: invitee.gender === GENDER.MALE ? 'rgba(8,111,111)' : 'rgba(111,18,8)'}"
    >
        {{ invitee.name }}
    </div>
</template>

<style scoped lang="scss">
    div {
        display: flex;
        justify-content: center;
        height: 40px;
        align-items: center;
        border-radius: 5px;
        margin-top: 15px;
        text-align: center;
        padding: 3px;
        color: aliceblue;
        background-color: aquamarine;
    }
</style>