<template>
  <div>
    <!--preson details starts here -->
    <div class="flex" v-for="person in personDetails" :key="person.name"> 
      <img
        class="mt-3 h-10 w-10 rounded-full"
        :src="person.imageUrl"
        width="500"
        height="600"
      />
      <div class="ml-2">
        <p>{{person.name}}</p>
      </div>
    </div>
    <!--preson details ends here -->
  </div>
</template>
<script lang='ts' setup>

const props = defineProps({
  /**
   * used for person details displayed in popup
   */
  personDetails:{
    type:Array,
    default:()=>[]
  }
})
</script>
