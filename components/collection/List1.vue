<template>
  <div class="px-4 sm:px-6 lg:px-8">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
        <h1 class="text-base font-semibold leading-6 text-gray-900">Users</h1>
        <p class="mt-2 text-sm text-gray-700">A list of all the users in your account including their name, title, email and role.</p>
      </div>
     
      <!-- <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button type="button" class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Add user</button>
      </div> -->
    </div>
    <div class="mt-8 flow-root">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
          <table class="min-w-full divide-y divide-gray-300">
            <thead>
              <tr>
                <th scope="col" class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0">Name</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">metric</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">age_of_property</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">lead_id</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">floor_plan_id</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">property_id</th>
                <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-0">
                  <span class="sr-only">Edit</span>
                </th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-200">
              <tr v-for="unit,index in units.data._rawValue" :key="index">
                <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0">{{ unit.name }}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ unit.metric }}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ unit.age_of_property }}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ unit.lead_id }}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ unit.floor_plan_id }}</td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ unit.property_id }}</td>
                <td class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-0">
                 <div class="flex">
      <PencilSquareIcon
              @click="emit('editUnits', unit, index,open)"
              class="h-5 w-5 mr-3"
              aria-hidden="true"
            ></PencilSquareIcon>
            <TrashIcon
              @click="deleteTemplate"
              class="h-5 w-5"
              aria-hidden="true"
            ></TrashIcon>
           
          </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'
import { XMarkIcon ,TrashIcon, PencilSquareIcon} from "@heroicons/vue/24/outline";


const props =defineProps({
    units:{
        type:Array,
        default:()=>[]
    },
     open:{
        type:Boolean,
        default:true
    }
})

const deleteUnits = (data: any) => {
};


</script>