<template>
  <div class="calendar-date-selector">
    <span @click="selectPrevious">Previous</span>
    <span @click="selectCurrent">Today</span>
    <span @click="selectNext">Next</span>
  </div>
</template>

<script>

export default {
  name: "CalendarModeSelector",

  props: {
    selectedMonth: {
      type: Number,
      required: true
    }
  },

  methods: {
    selectPrevious() {
      let newselectedMonth = 0;
      if (this.selectedMonth == 0) {
        newselectedMonth = 11;
      } else {
        newselectedMonth = this.selectedMonth - 1
      }
      this.$emit("monthSelected", newselectedMonth);
    },

    selectCurrent() {
      this.$emit("selectCurrent");
    },

    selectNext() {
      let newselectedMonth = 0;
      if (this.selectedMonth == 11) {
        newselectedMonth = 0;
      } else {
        newselectedMonth = this.selectedMonth + 1
      }
      this.$emit("monthSelected", newselectedMonth);
    }
  }
};
</script>

<style scoped>
.calendar-date-selector {
  display: flex;
  justify-content: space-between;
  width: 150px;
  color: var(--grey-800);
}

.calendar-date-selector > * {
  cursor: pointer;
  user-select: none;
}
</style>
