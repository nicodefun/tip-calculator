<script setup>
import { ref, watch } from "vue";
const tipArray = ref([5, 10, 15, 25, 50]);
const billNumber = ref(null);
const numOfPeople = ref(1);
const numIsZero = ref(false);
const tipAmount = ref(0);
const tipClass = ref(false);
const tipPercent = ref(null);
const editMode = ref(false);
const propsData = ref(props.data);
const props = defineProps({
  data: Object,
});

const emit = defineEmits(["sendData"]);

watch(
  [billNumber, numOfPeople, tipPercent],
  ([val, valN, valT]) => {
    const total = calTotalAmountPerPerson(valT, val, valN);
    tipAmount.value = (val*valT).toFixed(2);
    const tip = (tipAmount.value / valN).toFixed(2);
    propsData.value = { tip, total };
    emit("sendData", propsData.value);
  },
  { deep: true }
);

//methods
const addPeople = () => {
  numIsZero.value = false;
  editMode.value = true;

  if (numOfPeople.value <= 0) {
    numIsZero.value = true;
  }
  if (editMode.value) {
    tipPercent.value = 0.05;
  }
};
const calTotalAmountPerPerson = (tipPercent, amount, people) => {
  const total = (amount * tipPercent + amount) / people;
  return total.toFixed(2);
};
const chooseTip = (e) => {
  const index = e.target.id;
  tipPercent.value = (tipArray.value[index] / 100).toFixed(2);
  
};

const inputFocus = () => {
  tipPercent.value = 0.05;
};
</script>
<template>
  <section class="left-container">
    <div class="present">
      <small>Bill</small>
      <div class="present-child">
        <span class="dollar-sign"
          ><img src="../images/icon-dollar.svg" alt="dollar-sign"
        /></span>
        <input
          type="number"
          @focus="inputFocus"
          autofocus
          v-model="billNumber"
        />
      </div>
    </div>
    <div class="tip-selection">
      <small>Select Tip % {{ tipPercent }}</small>
      <ul>
        <li
          v-for="(tip, index) in tipArray"
          :id="index"
          :key="tip"
          @click="chooseTip"
          :class="tipClass?'active':''"
        >
          {{ tip }}%
        </li>
        <div class="show-tip">{{ tipAmount }}</div>
      </ul>
    </div>
    <div class="number-people">
      <div class="people-text">
        <small>Number of People</small>
        <p v-if="numIsZero">Can't be zero or empty</p>
      </div>
      <div class="people-grid">
        <span class="person-icon"
          ><img src="../images/icon-person.svg" alt="person-icon"
        /></span>
        <input
          type="number"
          v-model="numOfPeople"
          v-on:input="addPeople"
          @focusout="editMode = false"
          @keydown.enter="editMode = false"
          @focus="inputFocus"
          autofocus
        />
      </div>
    </div>
  </section>
</template>
<style scoped>
.left-container {
  width: 50%;
  /* background-color: rgb(221, 221, 231); */
  display: flex;
  flex-direction: column;
  margin: 2rem 2rem;
  justify-content: space-between;
}
small {
  color: #00474c;
  font-size: 1rem;
  font-family: inherit;
}
.tip-selection {
  width: 100%;
}

ul {
  width: 100%;
  list-style: none;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  padding-inline-start: 0;
  grid-row-gap: 1rem;
  align-content: center;
  column-gap: 1rem;
}
li {
  width: 100%;
  height: 100%;
  background-color: #00474c;
  border-radius: 0.5rem;
  align-items: center;
  display: flex;
  justify-content: center;
  font-weight: 800;
  padding: 0.5rem 0;
  font-size: 1.2rem;
  cursor: pointer;
}
li:hover,
li.active {
  background-color: #c5e4e7;
  color: #00474c;
}
.show-tip {
  background-color: #f7fafa;
  border-radius: 0.5rem;
  font-weight: 800;
  padding: 0.5rem 0;
  font-size: 1.2rem;
  color: #00474c;
  border: solid 2px #77d7df;
  border-radius: 0.2rem;
}

.present,
.tip-selection,
.number-people {
  width: 100%;
  display: flex;
  align-items: start;
  flex-direction: column;
}
.present-child,
.people-grid {
  display: flex;
  width: 100%;
  justify-content: space-between;
  align-items: center;
  padding: 0 1rem;
  height: 2.5rem;
  margin-bottom: 2rem;
}
.present-child {
  padding: 0;
  padding-left: 1rem;
  margin-top: 0.25rem;
  border: solid 2px #c5e4e7;
  border-radius: 0.2rem;
}
.present-child input {
  font-size: 1.5rem;
  font-weight: 800;
  color: #00474c;
}
.people-text {
  width: 100%;
  display: flex;
}
.people-text small,
.people-text p {
  width: 50%;
  padding: 0;
  align-items: start;
}
.people-text small {
  text-align: start;
}
.people-text p {
  padding: 0;
  margin: 0;
  text-align: end;
  color: orange;
}
.people-grid {
  margin-top: 0.25rem;
  border: solid 2px #c5e4e7;
  border-radius: 0.2rem;
  position: relative;
  padding: 0;
}
.people-grid.alert {
  border: solid 2px orange;
}
input:focus {
  outline: none !important;
}
.people-grid span {
  position: absolute;
  left: 1rem;
}
input {
  border: none;
  width: 100%;
  height: 100%;
  margin: 0;
  text-align: end;
  font-size: 1.2rem;
  color: #00474c;
  font-weight: 800;
  padding-right: 1rem;
  background-color: white;
}
</style>
