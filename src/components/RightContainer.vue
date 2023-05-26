<script setup>
import { ref } from "vue";

const data = ref({});
const props = defineProps({
  data: Object,
});

const emit = defineEmits(["resetData"]);

const reset = () => {
  data.value = {
    tip: 0.0,
    total: 0.0,
  };
  emit("resetData", data.value);
};
</script>
<template>
  <section class="right-container">
    <div class="right-container__top">
      <div class="tip-amount">
        <div class="tip-amount__text">
          <h3>Tip Amount</h3>
          <small>/ person</small>
        </div>
        <p class="tip-amount__total">${{ props.data.tip }}</p>
      </div>
      <div class="total-amount">
        <div class="total-amount__text">
          <h3>Total Amount</h3>
          <small>/ person</small>
        </div>
        <p class="total-amount__total">${{ props.data.total }}</p>
      </div>
    </div>
    <div class="right-container__bottom">
      <button @click="reset">RESET</button>
    </div>
  </section>
</template>

<style scoped>
.right-container {
  width: 50%;
  background-color: #00474c;
  display: flex;
  flex-direction: column;
  margin: 2.5rem 2rem;
  justify-content: space-between;
  border-radius: 2rem;
}
.right-container__top,
.right-container__bottom {
  height: 50%;
  display: flex;
  flex-direction: column;
}
.right-container__top {
  justify-content: space-around;
  padding-top: 5rem;
}
.right-container__bottom {
  justify-content: end;
  margin-bottom: 3rem;
}
.tip-amount,
.total-amount {
  width: 100%;
  display: flex;
  justify-content: space-between;
}
h3 {
  padding: 0;
  display: block;
}
small {
  display: block;
}
.tip-amount__text .tip-amount__text,
.tip-amount__total,
.total-amount__text,
.total-amount__total {
  width: 50%;
}
.tip-amount__text,
.total-amount__text {
  text-align: start;
  margin-left: 1.5rem;
}
.tip-amount__total,
.total-amount__total {
  width: 50%;
  font-size: 2rem;
  font-weight: 800;
  color: #2daea1;
  display: flex;
  justify-content: end;
  padding-right: 1.5rem;
}
button {
  color: #00474c;
  border: none;
  font-family: inherit;
  font-size: 1.2rem;
  font-weight: 800;
  margin: 0 1.5rem;
  background-color: #9fe8df;
  border-radius: 0.2rem;
  padding: 0.5rem 0;
}
</style>
