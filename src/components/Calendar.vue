<script>
export default {
  data() {
    return {
      days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
      currentYear: new Date().getFullYear(),
      currentMonth: new Date().getMonth(),
      currentDate: new Date().getUTCDate(),
    };
  },
  methods: {
    daysInMonth() {
      return new Date(this.currentYear, this.currentMonth + 1, 0).getDate();
    },
    startDay() {
      return new Date(this.currentYear, this.currentMonth, 1).getDay();
    },
    currentDateClass(num) {
      const calendarFullDate = new Date(
        this.currentYear,
        this.currentMonth,
        num
      ).toDateString();
      const currentFullDate = new Date().toDateString();
      return calendarFullDate === currentFullDate ? "border" : "";
    },
    prev() {
      if (this.currentMonth === 0) {
        this.currentMonth = 11;
        this.currentYear--;
      } else {
        this.currentMonth--;
      }
    },
    next() {
      if (this.currentMonth === 11) {
        this.currentMonth = 0;
        this.currentYear++;
      } else {
        this.currentMonth++;
      }
    },
  },
  computed: {
    currentMonthName() {
      return new Date(
        this.currentYear,
        this.currentMonth
      ).toLocaleString("default", { month: "long" });
    },
  },
};
</script>

<template>
  <div class="page">
    <h1>Calendar</h1>
    <section class="year">
      <h4>{{ currentMonthName }}</h4>
      <h4>{{ currentYear }}</h4>
    </section>
    <section class="week">
      <p class="weekday" v-for="day in days" :key="day">{{ day }}</p>
    </section>
    <section class="days">
      <p
        class="date-number"
        v-for="num in daysInMonth()"
        :key="num"
        :class="currentDateClass(num)"
      >
        {{ num }}
      </p>
    </section>
    <section class="buttons">
      <button @click="prev">Prev</button>
      <button @click="next">Next</button>
    </section>
  </div>
</template>

<style>
.page {
  margin: auto;
  display: flex;
  max-width: 400px;
  flex-direction: column;
  text-align: center;
}
.year {
  display: flex;
  justify-content: space-between;
  padding: 15px;
}
.week {
  display: flex;
  flex-direction: row;
  text-align: center;
}
.weekday {
  width: 14.28%;
}
.days {
  display: flex;
  flex-wrap: wrap;
  text-align: center;
  flex-direction: row;
}
.date-number {
  width: 14.28%;
}
.buttons {
  display: flex;
  justify-content: space-between;
}
</style>
