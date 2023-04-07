<template>
  <div class="w-[76rem]">
    <div class="bg-gray-50 mx-auto px-5 py-3 ">
      <div class="text-center mb-0 rounded-0">
        <!-- Input field for Template name -->
        <div class="flex justify-between items-center">
          <input
            id="name"
            v-model="templateName"
            type="text"
            name="name"
            class="block w-full rounded-md border-0 py-2 px-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            placeholder="Enter Template Name"
          />
        </div>
      </div>
    </div>
    <div class="mx-4 mt-4">
      <input
        id="subject"
        v-model="templateSubject"
        type="text"
        name="subject"
        class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6 w-[100%]"
        placeholder="Enter Template Name"
      />
      <!-- Textarea for template body -->
      <textarea
        id="body"
        v-model="templateBody"
        type="text"
        name="body"
        class="p-4 h-[calc(100vh-350px)] block w-full rounded-md border-0 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:py-1.5 sm:text-sm sm:leading-6"
        placeholder="Enter Template Name"
      />

      <div class="flex justify-end mr-3 mt-4">
        <button
          type="button"
          class="border rounded-md bg-white py-2 px-3 text-sm font-semibold text-gray-600 shadow-sm hover:bg-gray-50 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 mr-3"
        >
          Cancel
        </button>
        <button
          type="button"
          class="rounded-md bg-indigo-600 py-2 px-4 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          @click="addTemplate(templateId)"
        >
          Save
        </button>
      </div>
    </div>
  </div>
</template>
  <script setup lang="ts">
import { ref,defineEmits } from "vue";

const templateName = ref("");
const templateSubject = ref("");
const templateBody = ref("");

var emit =  defineEmits(['add_template'])

// Add Template to the template data
const addTemplate = (data: any) => {
  emit("add_template", {
    project_id: "12",
     name: templateName.value,
    subject: templateSubject.value,
    body: templateBody.value,
      is_active: "1",
      type: "PLAIN_TEXT",
      share_type: "PRIVATE",
      category: "Engineering",
   
  });
};
</script>