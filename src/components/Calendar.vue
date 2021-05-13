<script>
export default {
  data() {
    return {
      days: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
      currentYear: new Date().getFullYear(),
      currentMonth: new Date().getMonth(),
      currentDate: new Date().getUTCDate(),
      timeSVG: require("../assets/time.svg"),
    };
  },

  methods: {
    daysInMonth() {
      return new Date(this.currentYear, this.currentMonth + 1, 0).getDate();
    },
    startDay() {
      return new Date(this.currentYear, this.currentMonth, 0).getDay();
    },
    currentDateClass(num) {
      const calendarFullDate = new Date(
        this.currentYear,
        this.currentMonth,
        num
      ).toDateString();
      const currentFullDate = new Date().toDateString();
      return calendarFullDate === currentFullDate
        ? "text-primary font-weight-bold"
        : "";
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
      ).toLocaleString("en-US", { month: "long" });
    },
  },
};
</script>

<template>
  <div class="page d-flex justify-content-center align-items-center">
    <div
      class="left-container d-flex justify-content-center align-items-center"
    >
      <div class="m-4">
        <section>
          <img :src="timeSVG" class="time-svg" style="max-width: 275px" />
        </section>
      </div>
    </div>
    <div
      class="d-flex justify-content-center align-items-center"
      style="width: 50%"
    >
      <div
        class="time m-4 d-flex flex-column justify-content-center"
        style="max-width: 400px; min-width: 350px"
      >
        <h2>Calendar</h2>
        <section class="year d-flex justify-content-between p-2">
          <h4>{{ currentMonthName }}</h4>
          <h4>{{ currentYear }}</h4>
        </section>
        <section class="week d-flex flex-row text-center">
          <p
            class="weekday"
            style="width: 14.28%"
            v-for="(day, index) in days"
            :key="index"
          >
            {{ day }}
          </p>
        </section>
        <section class="days d-flex flex-row text-center flex-wrap">
          <p
            class="text-center"
            style="width: 14.28%"
            v-for="(start, index) in startDay()"
            :key="-1 - index"
          ></p>
          <p
            class="date-number"
            style="width: 14.28%"
            v-for="(num, index) in daysInMonth()"
            :key="index"
            :class="currentDateClass(num)"
          >
            {{ num }}
          </p>
        </section>
        <section class="buttons d-flex justify-content-between">
          <button @click="prev()">Prev</button>
          <button @click="next()">Next</button>
        </section>
      </div>
    </div>
  </div>
</template>

<style>
.page {
  flex-direction: row;
  min-height: 100vh;
}
.left-container {
  width: 50%;
}
.time {
  font-size: 20px;
}
@media only screen and (max-width: 767px) {
  .page {
    flex-direction: column !important;
  }
  .left-container {
    width: 100%;
  }
  .time {
    font-size: 14px;
  }
}
button {
  background: #536dfe;
  padding: 3px 15px 3px 15px;
  border: 1px solid #dde1ec;
  border-radius: 8px !important;
  color: #fff;
}
button:hover {
  background: #7086ff;
}
</style>
