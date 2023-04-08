<template>
  <div>
    <div class="mt-[-110rem] sm:ml-[118rem] sm:flex-none">
      <button
        @click="open = true"
        type="button"
        class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      >
        Add user
      </button>
    </div>
    <TransitionRoot as="template" :show="open">
      <Dialog as="div" class="relative z-10" @close="open = false">
        <div class="fixed inset-0" />

        <div class="fixed inset-0 overflow-hidden">
          <div class="absolute inset-0 overflow-hidden">
            <div
              class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10 sm:pl-16"
            >
              <TransitionChild
                as="template"
                enter="transform transition ease-in-out duration-500 sm:duration-700"
                enter-from="translate-x-full"
                enter-to="translate-x-0"
                leave="transform transition ease-in-out duration-500 sm:duration-700"
                leave-from="translate-x-0"
                leave-to="translate-x-full"
              >
                <DialogPanel class="pointer-events-auto w-screen max-w-2xl">
                  <div
                    class="flex h-full flex-col overflow-y-scroll bg-white py-6 shadow-xl"
                  >
                    <div class="px-4 sm:px-6">
                      <div class="items-start justify-between">
                        <div class="flex">
                          <DialogTitle
                            class="text-base font-semibold leading-6 text-white-900 mb-5"
                            >Add Candidates</DialogTitle
                          >
                          <div class="ml-[27.75rem] flex h-7 items-center">
                            <button
                              type="button"
                              class="rounded-md bg-indigo-700 text-indigo-200 hover:text-white focus:outline-none focus:ring-2 focus:ring-white"
                              @click="open = false"
                            >
                              <span class="sr-only">Close panel</span>
                              <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                            </button>
                          </div>
                        </div>
                        <hr />
                        <form>
                          <div class="mt-6 py-6">
                            <label />Candidate Name
                            <input
                              v-model="form.name"
                              type="text"
                              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                            />
                            <label for="test-type">Test Type</label>
                            <select
                              v-model="form.type"
                              id="test-type"
                              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                            >
                              <option value="practice">practice</option>
                              <option value="videoProfiles">
                                Video Profiles
                              </option>
                            </select>

                            <label />Max Time
                            <input
                              v-model="form.max_time_allowed"
                              type="number"
                              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                            />
                            <label />Due Date
                            <input
                              v-model="form.due_date"
                              type="datetime-local"
                              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                            />
                            <label />Difficulty Level
                            <select
                              v-model="form.difficulty_level"
                              id="level-type"
                              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                            >
                              <option value="Easy">Easy</option>
                              <option value="Hard">Hard</option>
                              <option value="Medium">Hard</option>
                            </select>
                            <label />Description
                            <textarea
                              v-model="form.description"
                              type="text"
                              class="p-4 block w-full rounded-md border-0 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:py-1.5 sm:text-sm sm:leading-6"
                            />
                            <label />Questions
                            <input
                              v-model="form.questions"
                              type="select"
                              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                            />
                            <label />No.of Attempts
                            <input
                              v-model="form.multiple_attempts_allowed"
                              type="number"
                              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                            />
                            <label />Instructions
                            <input
                              v-model="form.instructions"
                              type="select"
                              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                            />
                            <label />Status
                            <input
                              v-model="form.status"
                              type="number"
                              id="level-type"
                              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                            />
                            <label />Owner Id
                            <input
                              v-model="form.owner_id"
                              type="datetime-local"
                              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                            />
                            <label />last_modified_date
                            <input
                              v-model="form.last_modified_date"
                              type="datetime-local"
                              class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                            />
                          </div>
                        </form>
                      </div>
                    </div>
                    <div class="relative flex-1 px-2 sm:px-6">
                      <!-- Your content -->
                      <div class="bg-gray h-auto">
                        <div class="bg-gray-50 mx-auto px-4 py-3">
                          <div class="text-center mb-0 rounded-0">
                            <div class="flex justify-end mr-3 mt-[-3rem]">
                              <button
                                @click="open = false"
                                type="button"
                                class="border rounded-md bg-white py-2 px-3 text-sm font-semibold text-gray-600 shadow-sm hover:bg-gray-50 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 mr-3"
                              >
                                Cancel
                              </button>
                              <button
                                type="button"
                                class="rounded-md bg-indigo-600 py-2 px-4 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                                @click="addCandidates"
                              >
                                Save
                              </button>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </DialogPanel>
              </TransitionChild>
            </div>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
  </div>
</template>

<script setup>
import { ref, defineEmits, defineProps } from "vue";
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { XMarkIcon } from "@heroicons/vue/24/outline";

const props = defineProps({
  selectedBlocks: {
    type: Object,
    default: () => {},
  },
});
const emit = defineEmits(["add-candidates"]);

// Declaring the varibles
const open = ref(false);
const form = ref({
    name: "",
    type: "",
    max_time_allowed: 0,
    due_date: "2023-04-08T09:47:00.151Z",
    difficulty_level: "",
    description: "",
    questions: {},
    multiple_attempts_allowed: 0,
    instructions: {},
    status: 0,
    owner_id: "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    last_modified_date: "2023-04-08T09:47:00.151Z",
  })



//passing the data from emit for adding the blocks
const addCandidates = () => {
  emit("add-candidates", form.value);
  form.value = {};
  open.value = false;
};
</script>