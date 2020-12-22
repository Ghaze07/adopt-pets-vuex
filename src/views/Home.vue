<template>
  <div class="home">
    <h1>Adopt a New Best Friend.</h1>
    <div class="row">
      <div class="col col-md-6">
       <h5> Total Pets: {{animalsCount}}</h5>
      </div>
      <div class="col col-md-6">
        <h5>Number of cats: {{getAllCats.length}}</h5>
      </div>
    </div>

    <button @click="togglePetForm" class="btn btn-primary">Add Pet</button>

    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">

      <b-form-group id="input-group-2" label="Pet's Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="formData.name"
          placeholder="Enter name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="formData.species"
          :options="['cats', 'dogs']"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet's Age:" label-for="input-2">
        <b-form-input
          id="input-2"
          type="number"
          v-model="formData.age"
          placeholder="Enter Age"
          required
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" class="btn btn-success btn-sm mr-1" variant="success">Submit</b-button>
      <b-button type="reset" class="btn btn-danger btn-sm mr-1" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, name, age } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)

      // reset form after sumbit

      this.formData = {
        name: '',
        age: 0,
        species: null
      }
    }
  }
}
</script>
