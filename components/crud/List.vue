<template>
<div class="border m-5">
    <div class="sm:flex sm:items-center">
      <div class="sm:flex-auto">
         <div>
    <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Search</label>
    <div class="mt-2">
      <input type="email" name="email" id="email" class="block  rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" placeholder="search" />
    </div>
  </div>
        <h1 class="text-base font-semibold leading-6 text-gray-900">
          Users
        </h1>
        <p class="mt-2 text-sm text-gray-700">
          A list of all the Builders in your account including their name,
          email.
        </p>
      </div>
      <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
        <button
          @click="addUser"
          type="button"
          class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        >
          Add Builder
        </button>
      </div>
    </div>
<div class=" py-12 px-6">
  <ul role="list" class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3">
    <li
      v-for="(user,index) in users"
      :key="index"
      class="col-span-1 divide-y divide-gray-200 rounded-lg bg-white border"
    >
      <div class="flex w-full items-center justify-between space-x-6 p-6">
        <div class="flex-1 truncate">
          <div class="flex items-center space-x-3">
            <h3 class="truncate text-sm font-medium text-gray-900">
              {{ user.name }}
            </h3>
            <span
              class="inline-block flex-shrink-0 rounded-full bg-green-100 px-2 py-0.5 text-xs font-medium text-green-800"
              >{{ user.age }}</span
            >
          </div>
          <p class="mt-1 truncate text-sm text-gray-500">
            {{ user.date_of_birth }}
          </p>
        </div>
                            <PencilSquareIcon
                      @click="prefillData(user, index)"
                      class="h-5 w-5 mr-3"
                      aria-hidden="true"
                    ></PencilSquareIcon>
                    <TrashIcon
                      @click="
                        open=true
                      "
                      class="h-5 w-5"
                      aria-hidden="true"
                    ></TrashIcon>
        <!-- <img class="h-10 w-10 flex-shrink-0 rounded-full bg-gray-300" :src="person.imageUrl" alt="" /> -->
      </div>
      <TransitionRoot as="template" :show="open">
    <Dialog as="div" class="relative z-10" @close="open = false">
      <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0">
        <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" />
      </TransitionChild>

      <div class="fixed inset-0 z-10 overflow-y-auto">
        <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
          <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95" enter-to="opacity-100 translate-y-0 sm:scale-100" leave="ease-in duration-200" leave-from="opacity-100 translate-y-0 sm:scale-100" leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
            <DialogPanel class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6">
              <div class="sm:flex sm:items-start">
                <div class="mx-auto flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-full bg-red-100 sm:mx-0 sm:h-10 sm:w-10">
                  <ExclamationTriangleIcon class="h-6 w-6 text-red-600" aria-hidden="true" />
                </div>
                <div class="mt-3 text-center sm:ml-4 sm:mt-0 sm:text-left">
                  <DialogTitle as="h3" class="text-base font-semibold leading-6 text-gray-900">Deactivate account</DialogTitle>
                  <div class="mt-2">
                    <p class="text-sm text-gray-500">Are you sure you want to deactivate your account? All of your data will be permanently removed from our servers forever. This action cannot be undone.</p>
                  </div>
                </div>
              </div>
              <div class="mt-5 sm:mt-4 sm:flex sm:flex-row-reverse">
                <button type="button" class="inline-flex w-full justify-center rounded-md bg-red-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-red-500 sm:ml-3 sm:w-auto" @click="emit('deleteUser',index,open=false)">Deactivate</button>
                <button type="button" class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:mt-0 sm:w-auto" @click="open = false" ref="cancelButtonRef">Cancel</button>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
    </li>
  </ul>
  
  </div>
  </div>
</template>

<script setup lang='ts'>
import { defineProps ,defineEmits} from "vue";
import { ref } from 'vue'
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'
import { ExclamationTriangleIcon } from '@heroicons/vue/24/outline'
import {
  TrashIcon,
  PencilSquareIcon,
} from "@heroicons/vue/24/outline";

const open =ref(false)

const props = defineProps({
  users: {
    type: Array,
    default: () => [],
  },
});
const emit = defineEmits(["addUser","editUser","deleteUser"])

// add user details
const addUser = ()=>{
    emit ("addUser")
}

// prefill Data 
const prefillData=(data:any)=>{
    emit("editUser",data)
}
</script>