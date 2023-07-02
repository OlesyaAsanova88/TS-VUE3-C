<script setup lang="ts">
import {ref, computed} from "vue"
import Card from "./components/Card.vue"
import { GENDER, type Invitee } from '@/taype';

// enum GENDER {
//   MALE,
//   FEMALE
// }

// interface Invitee {
//   id: number;
//   name: string;
//   gender: GENDER
// }

const name = ref("");
const gender = ref(GENDER.MALE);
const invitees = ref<Invitee[]>([]);

const number = ref("");


const addInvitee = (): void => {
  if(name.value) {
    invitees.value.push({
      id: Math.floor(Math.random() * 1000000),
      name: name.value,
      gender: gender.value
    });
    name.value = '';
    gender.value = GENDER.MALE
  }
}

const count = computed<{
  female: number,
  male: number
}>(() => {
  return invitees.value.reduce((countObj, invitee) => {
    if(invitee.gender === GENDER.MALE) {
      return {
        ...countObj,
        male: countObj.male + 1
      }
    }
    return {
        ...countObj,
        female: countObj.male + 1
      }
  }, {male: 0, female: 0})
})

</script>

<template>
  <main class="wrapper">
    <div>

      <h1 
      class="wrapper__title"
      >
      People Invited to My Party
    </h1>
    <div class="wrapper__container">
      <input 
      v-model="name"
      class="wrapper__container_input"
      type="text" 
      placeholder="Name..."
      @keypress.enter="addInvitee"
      >
      <select 
      v-model="gender"
      class="wrapper__container_select"
      @keypress.enter="addInvitee"
      >
        <option :value="GENDER.MALE">Male</option>
        <option :value="GENDER.FEMALE">Female</option>
      </select>

      <!--Card-->
      <div class="wrapper__card">
        <Card 
        v-for="invitee in invitees"
        :key="invitee.id"
        :invitee="invitee"
        />
      </div>

      <!--Total -->

      <div class="wrapper__total">
        <p class="wrapper__total-text">Female - {{count.female}}</p>
        <p class="wrapper__total-text">Male - {{count.male}}</p>
      </div>

    </div>


<!--Угадай, сколько придет гостей-->
      <h2 
      class="wrapper__sb-title"
      >Guess my Favorite Number</h2>
      <input 
      class="wrapper__input"
      type="text"
      v-model="number"
      >
      <h2 
      v-if="number === '27'"
      class="wrapper__sb-title"
      >
      YOU GUESS IT!
    </h2>
    </div>
  
  </main>
</template>

<style scoped lang="scss">
  .wrapper {
    width: 1400px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 60px;
    gap: 30px;
    &__input {
      width: 480px;
      height: 30px;
      border: none;
      background: inherit;
      border-bottom: 1px solid gray;
      
    }
    &__input:focus {
      box-shadow: 0 0 15px aqua;
      outline: none;
    }

    &__sb-title {
      margin-bottom: 30px;
    }

    &__container {
      margin: 30px 0px;
    }

    &__container_input,
    &__container_select {
      width: 100%;
      padding: 5px;
      margin-bottom: 2px;
    }

    &__total {
      margin-top: 50px;
      
    }

    &__total-text {
      margin-bottom: 10px;
      font-size: 20px;
    }


  }
</style>
