<template>
  <div>
    <car-form :car="car" @onSubmit="onSubmit" @onReset="resetForm"></car-form>
  </div>
</template>

<script>
import CarForm from '../components/CarForm.vue'
import { cars } from '../services/cars'

export default {
  components: {
    CarForm
  },

  data () {
    return {
      car: this.getDefaultCar()
    }
  },

  created () {
    this.$route.params.id && cars.get(this.$route.params.id)
      .then((response) => {
        this.car = response.data
      })
  },

  methods: {
    onSubmit () {
      if (this.car.id) {
        this.editCar()
      } else {
        this.addCar()
      }
    },

    addCar () {
      cars.add(this.car)
        .then((success) => {
          this.redirectToCars()
        }).catch((error) => {
          console.log(error)
        })
    },

    editCar () {
      cars.edit(this.car)
        .then((success) => {
          this.redirectToCars()
        }).catch((error) => {
          console.log(error)
        })
    },

    resetForm () {
      this.car = this.getDefaultCar()
    },

    redirectToCars () {
      this.$router.push({ name: 'cars' })
    },

    getDefaultCar () {
      return {
        brand: '',
        model: '',
        maxSpeed: 200,
        year: 1990,
        isAutomatic: false,
        numberOfDoors: 4,
        engine: 'diesel'
      }
    }
  }
}
</script>

