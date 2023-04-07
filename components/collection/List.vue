
<template>
<div>
      <div
        v-for="template in emailTemplate.data._rawValue"
        :key="template.name"
        class="border p-4 rounded-md mb-3 shadow-sm bg-white"
      >
        <section>
          <h5 class="font-[500] text-md mb-2">{{ template.name }}</h5>
          <span class="text-gray-600">{{ template.subject }} </span>
          <span class="text-gray-600">{{ template.body }}</span>
          <div class="flex">
            <PencilSquareIcon
              @click="edit(template)"
              class="h-5 w-5"
              aria-hidden="true"
            ></PencilSquareIcon>
            <TrashIcon
              @click="deleteTemplate(template.uid)"
              class="h-5 w-5"
              aria-hidden="true"
            ></TrashIcon>
          </div>
        </section>
      </div>
      <div
        v-if="
          emailTemplate.data._rawValue &&
          emailTemplate.data._rawValue.length == 1
        "
      >
        <span
          ><div class="text-center">
            <svg
              class="mx-auto h-12 w-12 text-gray-400"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                vector-effect="non-scaling-stroke"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M9 13h6m-3-3v6m-9 1V7a2 2 0 012-2h6l2 2h6a2 2 0 012 2v8a2 2 0 01-2 2H5a2 2 0 01-2-2z"
              />
            </svg>
            <h3 class="mt-2 text-sm font-semibold text-gray-900">
              No templates found
            </h3>
            <p class="mt-1 text-sm text-gray-500">
              Get started by creating a new template.
            </p>
          </div>
        </span>
      </div>    
    </div>
</template>
  <script setup lang="ts">
import { ref } from "vue";
import { TrashIcon, PencilSquareIcon } from "@heroicons/vue/24/outline";
const show = ref(true);
const props = defineProps({
  // Get Template Mail Data
  emailTemplate: {
    type: Array,
    default:()=>[]
  },
});
console.log("emailTemplate",props.emailTemplate)

const deleteTemplate = (data: any) => {
   useAuthLazyFetchDelete(
    `https://v1-orm-lib.mars.hipso.cc/email-templates/${data}`,
 {}
  );
};
</script>