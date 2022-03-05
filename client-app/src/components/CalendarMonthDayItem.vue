<template>
  <li
    class="calendar-day"
    :class="{
      'calendar-day--not-current': notCurrent,
      'calendar-day--today': isToday
    }"
  >
    <span>{{ day }}</span>
  </li>
</template>

<script>

export default {
  name: "CalendarMonthDayItem",

  props: {
    day: {
      type: Number,
    },
    selectedMonth: {
      type: Number,
    },
    notCurrent: {
      type: Boolean,
    }
  },
  computed: {
    isToday() {
      const d = new Date();
      if (this.day === d.getDate() && this.selectedMonth === d.getMonth()) {
        return true
      }
      return false;
    },
  }
};
</script>

<style scoped>
.calendar-day {
  position: relative;
  min-height: 100px;
  font-size: 16px;
  background-color: #fff;
  color: var(--grey-800);
  padding: 5px;
}

.calendar-day > span {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  right: 2px;
  width: var(--day-label-size);
  height: var(--day-label-size);
}

.calendar-day--not-current {
  background-color: var(--grey-100);
  color: var(--grey-300);
}

.calendar-day--today {
  padding-top: 4px;
}

.calendar-day--today > span {
  color: #fff;
  border-radius: 9999px;
  background-color: var(--grey-800);
}
</style>
