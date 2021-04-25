<script>
export default {
  data() {
    return {
      days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
      currentYear: new Date().getFullYear(),
      currentMonth: new Date().getMonth() + 1,
      currentDate: new Date().getUTCDate(),
    };
  },
  methods: {
    daysInMonth() {
      return new Date(this.currentYear, this.currentMonth, 0).getDate();
    },
  },
};
</script>

<template>
  <div class="page">
    <h1>Calendar</h1>
    <section class="year">
      <h4>{{ currentMonth }}</h4>
      <h4>{{ currentYear }}</h4>
    </section>
    <section class="week">
      <p class="weekday" v-for="day in days" :key="day">{{ day }}</p>
    </section>
    <section class="days">
      <p class="date-number" v-for="date in daysInMonth()" :key="date">
        {{ date }}
      </p>
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
</style>
