<template>
  <div class="calendar-month">
    <div class="calendar-month-header">
      <CalendarDateIndicator
        :selectedMonth="months[selectedMonth]"
        class="calendar-month-header-selected-month"
      />

      <CalendarDateSelector
        :selectedMonth="selectedMonth"
        @monthSelected="selectMonth"
        @selectCurrent="setCurrentDate"
      />
    </div>

    <CalendarWeekdays />

    <ol class="days-grid">
      <CalendarMonthDayItem
        v-for="(day, index) in days"
        :key="index"
        :day="day"
        :selectedMonth="selectedMonth"
        :notCurrent="isNotCurrentMonth(index, day)"
        @dateSelected="selectDate"
      />
    </ol>
  </div>
</template>

<script>
import CalendarMonthDayItem from "./CalendarMonthDayItem";
import CalendarDateIndicator from "./CalendarDateIndicator";
import CalendarDateSelector from "./CalendarDateSelector";
import CalendarWeekdays from "./CalendarWeekdays";

export default {
  name: "CalendarMonth",

  components: {
    CalendarMonthDayItem,
    CalendarDateIndicator,
    CalendarDateSelector,
    CalendarWeekdays
  },

  data() {
    return {
      selectedMonth: 0,
      selectedDate: 1
    };
  },

  computed: {
    days() {
      //number of day in months
      let daysCount = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
      //get days for current month
      let daysArray = Array.from(Array(daysCount[this.selectedMonth]).keys(), (_, i) => i + 1)
      //get previous Month
      let previousMonth = this.selectedMonth === 0 ? 11 : this.selectedMonth - 1;
      //get random 0-2 number
      let number = Math.floor(Math.random() * 3);
      //add previous Month days into current month
      let previousDays = Array.from(Array(daysCount[previousMonth]).keys()).slice(daysCount[previousMonth] - number, daysCount[previousMonth]);
      daysArray.unshift(...previousDays);
      //add next month days
      daysArray.push(1, 2, 3, 4, 5, 6);

      return daysArray.slice(0, 35)
    },

    months() {
      return ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
    },
  },

  methods: {
    selectMonth(month) {
      this.selectedMonth = month;
    },
    selectDate(date) {
      this.selectedDate = date
    },
    setCurrentDate() {
      const d = new Date();
      this.selectedMonth = d.getMonth();
      this.selectedDate = d.getDate()
    },
    isNotCurrentMonth(index, date) {
      if (index >= 0 && index <= 6 && date > 9) {
        return true
      } else if (index >= 28 && index <= 34 && date < 10) {
        return true
      } else {
        return false
      }
    }
  }
};
</script>

<style scoped>
.calendar-month {
  position: relative;
  background-color: var(--grey-200);
  border: solid 1px var(--grey-300);
}

.day-of-week {
  color: var(--grey-800);
  font-size: 18px;
  background-color: #fff;
  padding-bottom: 5px;
  padding-top: 10px;
}

.day-of-week,
.days-grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
}

.day-of-week > * {
  text-align: right;
  padding-right: 5px;
}

.days-grid {
  height: 100%;
  position: relative;
  grid-column-gap: var(--grid-gap);
  grid-row-gap: var(--grid-gap);
  border-top: solid 1px var(--grey-200);
}
</style>
