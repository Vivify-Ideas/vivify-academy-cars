<template>
  <form @submit.prevent="onSubmit" @reset="onReset" class="jumbotron">
    <div class="form-group row">
      <label class="col-4 col-form-label" for="brand">Brand</label> 
      <div class="col-8">
        <input id="brand" name="brand" type="text" class="form-control here" required="required" minlength="2" v-model="car.brand">
      </div>
    </div>
    <div class="form-group row">
      <label for="model" class="col-4 col-form-label">Model</label> 
      <div class="col-8">
        <input id="model" name="model" type="text" class="form-control here" required="required" minlength="2" v-model="car.model">
      </div>
    </div>
    <div class="form-group row">
      <label for="year" class="col-4 col-form-label">Year</label> 
      <div class="col-8">
        <select id="year" name="year" class="custom-select" required="required" v-model="car.year">
          <option v-for="year in years" :value="year" :key="year">{{ year }}</option>
        </select>
      </div>
    </div>
    <div class="form-group row">
      <label for="speed" class="col-4 col-form-label">Maximum Speed</label> 
      <div class="col-8">
        <input id="speed" name="speed" type="number" class="form-control here" required="required" v-model="car.maxSpeed">
      </div>
    </div>
    <div class="form-group row">
      <label for="doors" class="col-4 col-form-label">Number of Doors</label> 
      <div class="col-8">
        <input id="doors" name="doors" type="number" class="form-control here" required="required" v-model="car.numberOfDoors">
      </div>
    </div>
    <div class="form-group row">
      <label class="col-4 col-form-label">Engine</label> 
      <div class="col-8">
        <div class="form-check">
          <label class="form-check-label">
            <input name="engine" type="radio" required="required" class="form-check-input" value="electric" v-model="car.engine">
            Electric
          </label>
        </div>
        <div class="form-check">
          <label class="form-check-label">
            <input name="engine" type="radio" required="required" class="form-check-input" value="petrol" v-model="car.engine">
            Petrol
          </label>
        </div>
        <div class="form-check">
          <label class="form-check-label">
            <input name="engine" type="radio" required="required" class="form-check-input" value="hybrid" v-model="car.engine">
            Hybrid
          </label>
        </div>
        <div class="form-check">
          <label class="form-check-label">
            <input name="engine" type="radio" required="required" class="form-check-input" value="diesel" v-model="car.engine">
            Diesel
          </label>
        </div>
      </div>
    </div>
    <div class="form-group row">
      <div class="col-4"></div> 
      <div class="col-8">
        <div class="form-check form-check-inline">
          <label class="form-check-label">
            <input name="automatic" type="checkbox" class="form-check-input" value="true" v-model="car.isAutomatic">
            Automatic
          </label>
        </div>
      </div>
    </div> 
    <div class="form-group row">
      <div class="offset-4 col-8">
        <button name="reset" type="reset" class="btn btn-default">Reset</button>
        <button name="preview" type="button" @click="preview" class="btn btn-default">Preview</button>
        <button name="submit" type="submit" class="btn btn-primary">Submit</button>
      </div>
    </div>
  </form>
</template>

<script>
import capitalize from 'lodash/capitalize'

export default {
  props: {
    car: Object
  },

  data () {
    return {
      years: Array(29).fill(1990).map((n, i) => n + i)
    }
  },

  methods: {
    onSubmit () {
      this.$emit('onSubmit')
    },

    onReset () {
      this.$emit('onReset')
    },

    preview () {
      alert(`
        Brand: ${this.car.brand}
        Model: ${this.car.model}
        Year: ${this.car.year}
        Maximum Speed: ${this.car.maxSpeed}
        Number of Doors: ${this.car.numberOfDoors}
        Engine: ${capitalize(this.car.model)}
        ${this.car.isAutomatic ? 'Automatic' : 'Manual'}
      `)
    }
  }
}
</script>
