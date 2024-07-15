<template>
  <section>
    <img :src="picture" :width="size" :height="size" ref="imageURL" /><br />

    <h1>ชื่อผู้สมัครงาน: {{ getFullName }}</h1>
    <h1>อายุ: {{ age }} ปี</h1>
    <h1>เงินเดือน: {{ salary }} บาท</h1>
    <h1>รายได้ต่อปี: {{ getIncome }} บาท</h1>
    <h1>ตำแหน่งงาน: {{ getDepartment }}</h1>

    <button @click="addSalary(5000)">เพิ่มเงินเดือน</button>
    <button @click="deSalary(5000)">ลดเงินเดือน</button>
    <button @click="toggleVisible">{{ isVisible ? "ซ่อน" : "แสดง" }}รายละเอียด</button>

    <div v-show="isVisible">
      <p>ที่อยู่: <span v-html="address"></span></p>
      <p>Social: <a :href="social" target="_blank">Facebook</a></p>
      <p v-if="hobby.length == 0">ไม่มีงานอดิเรก</p>
      <div v-else>
        <p>งานอดิเรก:</p>
        <ul>
          <li v-for="(item, index) in hobby" :key="index">{{ item }}</li>
        </ul>
      </div>
      <p>ข้อมูลพื้นฐาน:</p>
      <ul>
        <li v-for="(item, key) in general" :key="key">
          {{ key }} - {{ item }}
        </li>
      </ul>
    </div>

  </section>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      firstname: "Monkey",
      lastname: "D Luffy",
      age: 23,
      address: "<i>East Blue</i>",
      picture:
        "https://miro.medium.com/v2/resize:fit:736/1*YqfVlyCe06DfcPsR3kpYrw.jpeg",
      size: 200,
      social: "https://www.facebook.com",
      hobby: ["Fight", "Eat", "Sleep"],
      general: { gender: "Male", weight: 60, height: 170 },
      isVisible: false,
      salary: 20000
    };
  },

  methods: {
    toggleVisible() {
      this.isVisible = !this.isVisible
    },
    addSalary(value) {
      this.salary += value
    },
    deSalary(value) {
      this.salary -= value
    }
  },

  computed: {
    getFullName() {
      return `${this.firstname + " " + this.lastname}`
    },
    getIncome() {
      return this.salary * 12
    },
    getDepartment() {
      return this.salary >= 35000 ? "PM" : "SE"
    }
  },

  watch: {
    salary(value) {
      if (value > 50000) {
        alert("เงินเดือนไม่ควรเกิน 50,000 บาท")
        setTimeout(() => {
          this.salary = 20000
        }, 2000)
      }
    }
  }
};
</script>

<style>
</style>
