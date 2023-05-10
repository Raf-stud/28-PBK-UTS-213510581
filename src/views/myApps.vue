<template>
    <div class="container">
      <h1>TO-DO LIST PROJECT</h1>
      <section class="sesi1"> 
        <form @submit.prevent="addActivity">
          <input type="text" v-model="newActivity" placeholder="Add a task ">
          <button >Add</button>
        </form>
      </section>
      <section class="sesi2">
        <ul>
          <li v-for="(activity, index) in filteredActivities" :key="index" :class="{ done: activity.completed }">
            <div class="checkbox-wrapper-31">
              <input type="checkbox" v-model="activity.completed"/>
             <svg viewBox="0 0 35.6 35.6">
                <circle class="background" cx="17.8" cy="17.8" r="17.8"></circle>
                <circle class="stroke" cx="17.8" cy="17.8" r="14.37"></circle>
                <polyline class="check" points="11.78 18.12 15.55 22.23 25.17 12.87"></polyline>
             </svg>
          </div>
            <span>{{ activity.text }}</span>
            <button @click="removeActivity(index)">Remove</button>
          </li>
        </ul>
      </section>
   
     <section class="sesi3">
        <label>Show only unfinished activities:</label>
        <input type="checkbox" v-model="showUnfinished">
      </section>
    </div>
  </template>
  
  <script>
  export default{
  data(){
    return {
        newActivity: '',
        activities: [
          { text: 'Sholat 5 waktu', completed: false },
          { text: 'sarapan pagi ', completed: true },
          { text: 'hunting thr', completed: false }
        ],
        showUnfinished: false
      }
    },
    methods: {
      addActivity() {
        if (this.newActivity.trim() !== '') {
          this.activities.push({ text: this.newActivity, completed: false });
          this.newActivity = '';
        }
      },
      removeActivity(index) {
        this.activities.splice(index, 1);
      }
    },
    computed: {
      filteredActivities() {
        if (this.showUnfinished) {
          return this.activities.filter(activity => !activity.completed);
        } else {
          return this.activities;
        }
      }
    }
  }
  </script>
  
  <style>
  
  
  body{
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #e32688;
  }
  
  .done {
    text-decoration: line-through;
    text-decoration-color: #031343;
  }
  
  input[type="text"]::placeholder {
    color: blue;
  }
  ul {
    list-style: none;
  }
  .checkbox-wrapper-31:hover .check {
      stroke-dashoffset: 0;
    }
  
    .checkbox-wrapper-31 {
      position: relative;
      display: inline-block;
      width: 40px;
      height: 40px;
    }
    .checkbox-wrapper-31 .background {
      fill: #ccc;
      transition: ease all 0.6s;
      -webkit-transition: ease all 0.6s;
    }
    .checkbox-wrapper-31 .stroke {
      fill: none;
      stroke: #fff;
      stroke-miterlimit: 10;
      stroke-width: 2px;
      stroke-dashoffset: 100;
      stroke-dasharray: 100;
      transition: ease all 0.6s;
      -webkit-transition: ease all 0.6s;
    }
    .checkbox-wrapper-31 .check {
      fill: none;
      stroke: #fff;
      stroke-linecap: round;
      stroke-linejoin: round;
      stroke-width: 2px;
      stroke-dashoffset: 22;
      stroke-dasharray: 22;
      transition: ease all 0.6s;
      -webkit-transition: ease all 0.6s;
    }
    .checkbox-wrapper-31 input[type=checkbox] {
      position: absolute;
      width: 100%;
      height: 100%;
      left: 0;
      top: 0;
      margin: 0;
      opacity: 0;
      -appearance: none;
      -webkit-appearance: none;
    }
    .checkbox-wrapper-31 input[type=checkbox]:hover {
      cursor: pointer;
    }
    .checkbox-wrapper-31 input[type=checkbox]:checked + svg .background {
      fill: #6cbe45;
    }
    .checkbox-wrapper-31 input[type=checkbox]:checked + svg .stroke {
      stroke-dashoffset: 0;
    }
    .checkbox-wrapper-31 input[type=checkbox]:checked + svg .check {
      stroke-dashoffset: 0;
    }
  
  
  
  </style>
  