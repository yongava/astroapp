<template>
  <div class="container">
    <div class="bg-img"></div>
    <div class="page-container">
      <h1 class="page-headline">Select Your Birth Date</h1>
      <div class="select_container">
        <div class="custom-select" id="select-month" @click="toggleDropdown('month')" style="z-index: 5001;">
          <input class="chosen-value" type="text" v-model="selectedMonth" placeholder="Select Month" readonly>
          <ul class="value-list" v-show="isMonthDropdownOpen">
            <li v-for="(month, index) in months" :key="index" @click="selectMonth(month)">{{ month }}</li>
          </ul>
        </div>
        <div class="custom-select" id="select-date" @click="toggleDropdown('date')" style="z-index: 5000;">
          <input class="chosen-value" type="text" v-model="selectedDate" placeholder="Select Date" readonly>
          <ul class="value-list" v-show="isDateDropdownOpen">
            <li v-for="date in dates" :key="date" @click="selectDate(date)">{{ date }}</li>
          </ul>
        </div>
      </div>
      <div class="btn-container">
        <button type="button" class="submit-btn" @click="submitDate">Submit</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedMonth: '',
      selectedDate: '',
      isMonthDropdownOpen: false,
      isDateDropdownOpen: false,
      months: [
        "January", "February", "March", "April", "May", "June",
        "July", "August", "September", "October", "November", "December"
      ],
      dates: Array.from({ length: 31 }, (_, i) => i + 1)
    };
  },
  methods: {
    toggleDropdown(type) {
      if (type === 'month') {
        this.isMonthDropdownOpen = !this.isMonthDropdownOpen;
        this.isDateDropdownOpen = false;
      } else {
        this.isDateDropdownOpen = !this.isDateDropdownOpen;
        this.isMonthDropdownOpen = false;
      }
    },
    selectMonth(month) {
      this.selectedMonth = month;
      this.isMonthDropdownOpen = false;
    },
    selectDate(date) {
      this.selectedDate = date;
      this.isDateDropdownOpen = false;
    },
    submitDate() {
      alert(`Selected Date: ${this.selectedMonth} ${this.selectedDate}`);
      // Add your submit logic here
    },
    handleClickOutside(event) {
      if (!this.$el.contains(event.target)) {
        this.isMonthDropdownOpen = false;
        this.isDateDropdownOpen = false;
      }
    }
  },
  mounted() {
    document.addEventListener('click', this.handleClickOutside);
  },
  beforeUnmount() {
    document.removeEventListener('click', this.handleClickOutside);
  }
};
</script>

<style scoped>
body {
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f0f0f0;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100%;
  position: relative;
}

.bg-img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: url('background.jpg') no-repeat center center/cover;
  z-index: -1;
  opacity: 0.5;
}

.page-container {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.page-headline {
  font-size: 24px;
  margin-bottom: 20px;
}

.select_container {
  margin-bottom: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.custom-select {
  position: relative;
  display: inline-block;
  width: 150px;
  margin: 0 10px;
}

.custom-select input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  cursor: pointer;
}

.value-list {
  position: absolute;
  width: 100%;
  border: 1px solid #ccc;
  border-top: none;
  max-height: 150px;
  overflow-y: auto;
  background-color: white;
  z-index: 1000;
}

.value-list li {
  padding: 10px;
  cursor: pointer;
}

.value-list li:hover {
  background-color: #f0f0f0;
}

.btn-container {
  margin-top: 20px;
}

.submit-btn {
  padding: 10px 20px;
  background-color: #555;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.submit-btn:hover {
  background-color: #9f4c3c;
}
</style>
