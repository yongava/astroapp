<template>
  <div class="container">
    <div class="logo-section">
      <img
        src="mascot.png"
        alt="Discover yours in just a few seconds."
        id="company-logo"
        width="150"
        height="150"
      />
    </div>
    <div class="title-section">
      <h2>Select Your Birth Date</h2>
    </div>
    <div class="input-section">
      <select v-model="selectedMonth">
        <option v-for="(month, index) in months" :key="index" :value="month">{{ month }}</option>
      </select>
      <select v-model="selectedDate">
        <option v-for="date in dates" :key="date" :value="date">{{ date }}</option>
      </select>
      <button @click="submitDate">Submit</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedMonth: null,
      selectedDate: null,
      months: [
        "January", "February", "March", "April", "May", "June",
        "July", "August", "September", "October", "November", "December"
      ],
      dates: Array.from({ length: 31 }, (_, i) => i + 1)
    };
  },
  methods: {
    submitDate() {
      console.log(`Selected Date: ${this.selectedMonth} ${this.selectedDate}`);
      // Add your submit logic here
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1rem;
}

.logo-section {
  display: flex;
  justify-content: center;
  width: 100%;
  margin-bottom: 1rem;
}

#company-logo {
  width: 150px;
  height: auto;
  border-radius: 100px;
}

.title-section {
  margin-bottom: 1rem;
}

.title-section h2 {
  font-size: 24px;
  font-weight: bold;
  text-align: center;
}

.input-section {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.input-section select {
  margin: 0.5rem 0;
  padding: 0.5rem;
  border-radius: 5px;
  border: 1px solid #ddd;
  font-size: 16px;
}

.input-section button {
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  background-color: #555555;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.input-section button:hover {
  background-color: #9f4c3c;
}
</style>
