<script setup lang="ts">
import { type } from 'os'
import { ref } from 'vue'

/**
 * Restaurants
 *
 * @param {string} name
 */

interface Restaurant {
  name?: string
  address?: string
  status?: RestaurantStatus
  dishes?: Dish[]
}

// const All_Status = [ 'Want to Try','Recommended','Do Not Recommended',,'Must Try']

type RestaurantStatus = 'Want to Try' | 'Recommended' | 'Do Not Recommended' | 'Must Try'

const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})

//How to extract value from type
const statusList = ['Want to Try', 'Recommended', 'Do Not Recommended', 'Must Try']

function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    address: '',
    status: 'Want to Try',
    dishes: []
  })
  newRestaurant.value.name = ''
}
</script>

<template>
  <main>
    <pre>
      {{ newRestaurant }}
    </pre>
    <!---Create a form that allows users to add a restaurant to a list-->

    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name</label>
        <input id="restaurant-name" v-model="newRestaurant.name" type="text" />
        <button type="submit">Add Restaurant</button>
      </div>

      <div>
        <label for="restaurant-address">Restaurant Address</label>
        <input id="restaurant-address" v-model="newRestaurant.address" type="text" />
        <button type="submit">Add Restaurant</button>
      </div>

      <div>
        <label for="restaurant-status">Restaurant Status</label>
        <select name="restaurant-status" id="restaurant.status" v-model="newRestaurant.status">
          <option v-for="status in statusList" :value="status" :key="status">
            {{ status }}
          </option>
        </select>
        <button type="submit">Add Restaurant</button>
      </div>
    </form>

    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant.name">{{ restaurant.name }}</li>
    </ul>
  </main>
</template>
