<template>
  <BuildersList
    :getBuilders="getBuildersData"
    @addBuilderSidebar="addBuilderSidebar"
    @editData="openEditSidebar"
    @deleteData="deleteBuilder"
  />

  <div v-if="is_sidebar" :key="render">
    <BuildersAdd @builderPostBody="addBuilder" />
  </div>

  <div v-if="isEdit" :key="render">
    <BuildersEdit @builderEditBody="editBuilder" :prefillData="prefillData" />
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
const is_sidebar = ref(false);
const render = ref(0);
const isEdit = ref(false);
const prefillData = ref({});
let getBuildersData = ref("");

//open customfields sidebar
const addBuilderSidebar = () => {
  is_sidebar.value = true;
  render.value++;
};
const openEditSidebar = (data: any) => {
  isEdit.value = true;
  render.value++;
  prefillData.value = { ...data };
};
const url = "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/";

const authHeader = {
  "Content-Type": "application/json",
  Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNmZlZDJiYTgwYThkNGM0MjlhZGZiOGQ1ZTZmZTY0ODAiLCJkIjoiMTY4MDA4NCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzk3Mjl9.5cJkrudAvTWoVRigTNcfQ321W_lOyMm-xsb9rMxuVBE`,
};

const getOptions = {
  method: "GET",
  headers: authHeader,
};
const { data: getData } = await useAuthLazyFetch(
  "https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  getOptions
);

getBuildersData.value = getData.value;

//  add call for builder data
const addBuilder = async (body: Object) => {
  const options = {
    method: "POST",
    headers: authHeader,
    body: JSON.stringify(body),
  };
  await useAuthLazyFetchPost(`${url}`, options);
  getBuildersData.value.unshift(body);
  is_sidebar.value = false;
};
// Edit call for builder data
const editBuilder = async (body: Object) => {
  const editOptions = {
    method: "PUT",
    headers: authHeader,
    body: JSON.stringify(body),
  };
  await useAuthLazyFetchPut(`${url}${body.uid}`, editOptions);
  isEdit.value = false;
};

// Delete Call for builder data
const deleteBuilder = async (data: any, index: number) => {
  const deleteOptions = {
    method: "DELETE",
    headers: authHeader,
  };
  await useAuthLazyFetchDelete(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/builder/${data.uid}`,
    deleteOptions
  );
  getBuildersData.value.splice(index, 1);
};
</script>