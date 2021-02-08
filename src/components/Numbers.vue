<template>
  <div>
    <div
      class="number"
      :id="'number-' + number"
      v-for="number in n"
      :key="number"
      @mouseover="hov(number)"
      @mouseout="reset"
    >
      {{ number }}
    </div>
  </div>
</template>

<script>
export default {
  /*Since the child component is nested into the parent component,
  using a prop as way to pass data (limit) from the parent component 
  to the child component is the best idea.*/
  props: {
    limit: {
      type: Number,
    },
  },
  data() {
    return {
      numbers: [],
    };
  },
  methods: {
    hov(number) {
      const nums = document.querySelectorAll(".number");

      for (let i = 0; i < nums.length; i++) {
        const num = nums[i].textContent.trim();
        if (number % num === 0) {
          nums[i].classList.add("active");
        }
      }
    },
    reset() {
      const nums = document.querySelectorAll(".number");
      nums.forEach((num) => num.classList.remove("active"));
    },
  },
  /* The function n(), does not receive any parameters, is doing complex calculations 
  and always reacts to the data changes since the limit property value is always 
  changing. Hence, it's a better idea to use the function n() as a computed property rather than a method.*/
  computed: {
    n() {
      let numbers = [];
      for (var i = 0; i < this.limit; i++) {
        numbers = [...numbers, i];
      }
      return numbers.sort(() => Math.random() - 0.5);
    },
  },
};
</script>

<style scoped>
.number {
  display: inline-block;
  padding: 5px;
  background-color: lightgrey;
  margin: 5px;
  transition: all 0.3s ease-in-out;
}

.number:hover {
  background-color: #0d0b0b;
  color: #ffffff;
  cursor: pointer;
  transform: scale(1.2);
}

.active {
  background-color: #690303;
  color: #ffffff;
}
</style>
