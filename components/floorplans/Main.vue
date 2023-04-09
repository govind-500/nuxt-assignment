<template>
  <div>
    <FloorplansList
      @slidebar="addSlidebar"
      @editSlidebar="editSlidebar"
      @deleteFloors="deleteFloors"
      :floorData="getFloorData"
    ></FloorplansList>
    <div v-if="is_open" :key="render">
      <FloorplansAdd
        @add-floors="addFloors"
        :floorData="getFloorData"
        :is_open="is_open"
      ></FloorplansAdd>
    </div>
    <div v-if="is_open_edit" :key="editRender">
      <FloorplansEdit
        :floorData="getFloor"
        @editFloors="editFloors"
      ></FloorplansEdit>
    </div>
  </div>
</template>
<script setup lang='ts'>
import { Body } from "nuxt/dist/head/runtime/components";
import { ref } from "vue";

const getFloorData = ref([]);
const is_open = ref(false);
const is_open1 = ref(false);
const render = ref(0);
const editRender = ref(0);
const getFloor = ref({});
const is_open_edit = ref(false);
// for getting data from get call
const getData = async () => {
  const { data: floorData } = await useAuthLazyFetch(
    "https://v1-orm-gharpe.mercury.infinity-api.net/api/floorplans/?offset=0&limit=100&sort_column=id&sort_direction=desc",
    {}
  );
  getFloorData.value = floorData.value;
};

// add call for adding the candidates
const addFloors = async (data: object) => {
  console.log("addDataaaa", data);
  const postOptions = {
    body: JSON.stringify(data),
  };
  // post call for adding blocks
  await useAuthLazyFetchPost(
    "https://v1-orm-gharpe.mercury.infinity-api.net/api/floorplans/",
    postOptions
  );
  getFloorData.value.unshift(data);
  getData();
};
getData();

// Add openSlidebar data
const addSlidebar = () => {
  is_open.value = true;
  render.value++;
};

//edit openslidebar data
const editSlidebar = (data: any) => {
  getFloor.value = data;
  editRender.value++;
  is_open_edit.value = true;
};
const editFloors = async (data: any) => {
  console.log("EditDataa", data);
  const putOptions = {
    body: JSON.stringify(data),
  };
  await useAuthLazyFetchPut(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/floorplans/${data.uid}`,
    putOptions
  );
  getData();
};
const deleteFloors= async(data:any)=>{
  console.log("deleteeeeeee",data);
  const deleteOptions = {
    body: JSON.stringify(data),
  };
  await useAuthLazyFetchDelete(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/floorplans/${data.uid}`,
    deleteOptions
  );
  getData();
}
</script>