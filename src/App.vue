<script setup>
import Workout from './components/Workout.vue'
</script>

<template>
    <!-- Default View listing workouts-->
    <div v-if="state === null" class="hero min-h-screen card shadow-2xl bg-base-100">
      <div class="hero-content flex-col">
        <div class="text-center">
          <h1 class="text-5xl font-bold">Weightlifting App</h1>
          <p class="py-6">Add a new workout or select one from the list below to view details.</p>
        </div>
        <div>
          <div class="card-body">
            <div  v-for="(workout, index) in this.workouts" :key="workout.id" class="m-2">
              <div class="indicator">
                <span class="indicator-item badge badge-secondary">{{ workout.date }}</span>
                <div>
                  <button class="btn btn-primary">{{ workout.title }}</button>
                </div>
              </div>
            </div>
          </div>
          <div class="form-control mt-6">
            <button @click="addWorkout" class="btn btn-secondary">Add New</button>
          </div>
        </div>
      </div>
    </div>
    <!-- Add Workout View with from for user input-->
    <div v-if="state === 'add'" class="hero min-h-screen">
      <div class="hero-content flex-col lg:flex-row-reverse">
        <div class="text-center lg:text-left">
          <h1 class="text-5xl font-bold">Add New Workout</h1>
        </div>
        <div class="card flex-shrink-0 w-full shadow-2xl bg-base-100">
          <div class="card-body">
            <div class="form-control">
              <label class="label">
                <span class="label-text">Title</span>
              </label>
              <input v-model="newWorkout.title" type="text" placeholder="title" class="input input-bordered" />
            </div>
            <div class="form-control">
              <label class="label">
                <span class="label-text">Date</span>
              </label>
              <input v-model="newWorkout.date" type="text" placeholder="date" class="input input-bordered" />
            </div>
            <div class="form-control mt-6">
              <button @click="handleSubmit" class="btn btn-secondary">Add Workout</button>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
  export default {
    name: 'exercise app',
    data() {
      return {
        state: null,
        selected: null,
        newWorkout: {
          title: '',
          date: ''
        },
        workouts: [
          {
            id: 1,
            title: "Workout 1",
            date: 'Jan 1',
            exercises: []
          },
          {
            id: 2,
            title: "Workout 2",
            date: 'Jan 2',
            exercises: []
          },
          {
            id: 3,
            title: "Workout 3",
            date: 'Jan 3',
            exercises: []
          },
          {
            id: 4,
            title: "Workout 4",
            date: 'Jan 4',
            exercises: []
          }
        ]
      }
    },
    methods: {
      handleSubmit() {
        if (this.newWorkout.title !== '' || this.newWorkout.date !== '') {
          this.workouts = [...this.workouts, {
          id: this.workouts.length + 1,
          title: this.newWorkout.title,
          date: this.newWorkout.date,
          exercises: []
          }]
          this.state = null
        }
      },
      addWorkout() {
        this.state = 'add'
      }
    }
  }
</script>
