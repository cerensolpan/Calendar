<script>
// @ is an alias to /src
import Calendar from "@/components/Calendar.vue";

export default {
  name: "calendar",
  components: {
    Calendar,
  },
};
</script>

<template>
  <div class="calendar">
    <Calendar />
  </div>
</template>
