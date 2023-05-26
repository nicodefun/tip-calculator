<script setup>
import LeftContainer from "./components/LeftContainer.vue";
import RightContainer from "./components/RightContainer.vue";
import { ref } from "vue";

components: {
  LeftContainer, RightContainer;
}

const data = ref({
  tip: 0.0,
  total: 0.0,
});

const getData = (d) => {
   data.value = d;
};

const resetData = (d)=>{
  data.value = d;
}

</script>

<template>
  <div>
    <div class="splitter">
      <p class="spli">SPLI</p>
      <p>TTER</p>
    </div>
    <main>
      <left-container :data="data" @send-data="getData"></left-container>
      <right-container :data="data"  @reset-data="resetData"></right-container>
    </main>
  </div>
</template>

<style scoped>
main {
  width: 50rem;
  min-height: 50vh;
  background-color: white;
  border-radius: 2rem;
  box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
  display: flex;
  overflow: hidden;
}
.splitter {
  margin-bottom: 2rem;
  font-size: 1.5rem;
  font-weight: 700;
  color: #476a6a;
  display: flex;
  flex-direction: column;
  letter-spacing: 0.5rem;
  align-items: stretch;
}
p {
  margin: 0.2rem;
}
.spli {
  transform: translateX(-2px);
}
</style>
