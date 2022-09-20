<script setup lang="ts">
interface Entry {
  due: number;
  worked: number;
}
interface DayEntry extends Entry {
  date: Date;
}
interface WeekEntry extends Entry {
  days: DayEntry[];
  balance: number;
  weekNumber: number;
}

interface HoursYear {
  balance: number;
  weeks: WeekEntry[];
}

const calendar = () => {
  const calendarYear: HoursYear = {
    weeks: [],
    balance: 0,
  };
  const date = new Date(2021, 11, 27);
  let weekNumber = 1;
  while (date.getFullYear() <= 2022) {
    const currentWeek: WeekEntry = {
      days: [],
      due: 0,
      worked: 0,
      balance: 0,
      weekNumber: weekNumber,
    };
    let weekday = 0;
    while (weekday < 7) {
      const day: DayEntry = {
        date: new Date(date),
        due: weekday < 5 ? 8 : 0,
        worked: weekday < 5 ? 8 : 0,
      };
      currentWeek.days.push(day);
      currentWeek.due += day.due;
      currentWeek.worked += day.worked;
      currentWeek.balance = day.worked - day.due;
      date.setDate(date.getDate() + 1);
      weekday++;
    }
    weekNumber++;
    calendarYear.weeks.push(currentWeek);
  }
  return calendarYear;
};
</script>
<template>
  <div class="table-container">
    <table class="table">
      <thead>
        <tr>
          <td>KW</td>
          <td>Män</td>
          <td>Zis</td>
          <td>Mit</td>
          <td>Dun</td>
          <td>Fri</td>
          <td>Sam</td>
          <td>Sun</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="week in calendar().weeks" :key="week">
          <td>{{ week.weekNumber }}</td>
          <td v-for="day in week.days" :key="day">
            <p>{{ day.date.toDateString() }}</p>
            <p>hours due: {{ day.due }}</p>
            <p>hours worked: {{ day.worked }}</p>
          </td>
          <td>total due: {{ week.due }}</td>
          <td>total worked: {{ week.worked }}</td>
          <td>Balance: {{ week.balance }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
