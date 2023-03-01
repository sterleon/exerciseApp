<template>
    <div class="indicator">
        <span class="indicator-item badge badge-secondary">{{ workoutObj.date }}</span>
        <div>
            <button class="btn btn-primary">{{ workoutObj.title }}</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'workout',
        props: {
            workoutObj: Object
        },
        data() {
            return {

            }
        }
    }
</script>