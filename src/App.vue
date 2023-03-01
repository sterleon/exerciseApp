<script setup>
import Workout from './components/Workout.vue'
</script>

<template>
    <!-- Default View listing workouts-->
    <div v-if="state === null" class="hero card shadow-2xl bg-base-100">
      <div class="hero-content flex-col">
        <div class="text-center">
          <h1 class="text-5xl font-bold">Weightlifting App</h1>
          <p class="py-6">Add a new workout or select one from the list below to view details.</p>
        </div>
        <div>
          <div class="card-body">
            <div  v-for="(workout, index) in this.workouts" :key="workout.id" class="m-2">
              <Workout @click="handleWorkoutClick(index)" v-bind:workoutObj="workout" />
            </div>
          </div>
          <div class="form-control mt-6">
            <button @click="this.state = 'add'" class="btn btn-secondary">Add New</button>
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
    <!-- Single Workout Detail View -->
    <div v-if="state === 'workout'" class="rounded-md hero bg-base-200">
      <div class="hero-content text-center">
        <div>
          <h1 class="text-5xl font-bold">{{ this.workouts[this.selected].title }}</h1>
          <h2>{{ this.workouts[this.selected].date }}</h2>
          <div class="overflow-x-auto">
            <table class="table w-full">
              <!-- head -->
              <thead>
                <tr>
                  <th></th>
                  <th>Exercise</th>
                  <th>Sets</th>
                  <th>Reps</th>
                  <th>Weight</th>
                </tr>
              </thead>
              <tbody v-for="(exercise, index) in this.workouts[this.selected].exercises" :key="exercise.id">
                <tr>
                  <th>{{ exercise.id }}</th>
                  <td>{{ exercise.name }}</td>
                  <td>{{ exercise.sets }}</td>
                  <td>{{ exercise.reps }}</td>
                  <td>{{ exercise.weight }}</td>
                </tr>
              </tbody>
            </table>
          </div>
          <button @click="this.state = 'addExercise'" class="btn btn-secondary mt-2 mr-1">Add Exercise</button>
          <button @click="this.state = null" class="btn btn-secondary mt-2 ml-1">Back to Workouts</button>
        </div>
      </div>
    </div>
    <!-- Add Exercise View -->
    <div v-if="state === 'addExercise'" class="hero">
      <div class="hero-content flex-col">
        <div class="text-center">
          <h1 class="text-5xl font-bold">Add New Exercise</h1>
        </div>
        <div class="card flex-shrink-0 w-full shadow-2xl bg-base-100">
          <div class="card-body">
            <div class="form-control">
              <label class="label">
                <span class="label-text">Name</span>
              </label>
              <input v-model="newExercise.name" type="text" class="input input-bordered" />
            </div>
            <div class="form-control">
              <label class="label">
                <span class="label-text">Sets</span>
              </label>
              <input v-model="newExercise.sets" type="text" class="input input-bordered" />
            </div>
            <div class="form-control">
              <label class="label">
                <span class="label-text">Reps</span>
              </label>
              <input v-model="newExercise.reps" type="text" class="input input-bordered" />
            </div>
            <div class="form-control">
              <label class="label">
                <span class="label-text">Weight</span>
              </label>
              <input v-model="newExercise.weight" type="text" class="input input-bordered" />
            </div>
            <div class="form-control mt-6">
              <button @click="handleAddExercise" class="btn btn-secondary">Add</button>
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
        newExercise: {
          name: '',
          sets: '',
          reps: '',
          weight: ''
        },
        workouts: []
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
      handleWorkoutClick(i) {
        this.state = 'workout'
        this.selected = i
      },
      handleAddExercise() {
        this.workouts[this.selected].exercises = [
          ...this.workouts[this.selected].exercises,
          {
            id: this.workouts[this.selected].exercises.length + 1,
            name: this.newExercise.name,
            sets: this.newExercise.sets,
            reps: this.newExercise.reps,
            weight: this.newExercise.weight
          }
        ]
        this.state = 'workout'
      }
    }
  }
</script>
