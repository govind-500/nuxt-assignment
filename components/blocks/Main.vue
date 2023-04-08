<template>
  <div>
    <BlocksList
      :blocksData="blocksData"
      @deleteRecord="deleteBlocks"
      @prefillData="prefillData"
    ></BlocksList>
    <div>
      <BlocksAdd
        :selectedBlocks="selectedBlocks"
        @add-blocks="addBlocks"
      ></BlocksAdd>
      <BlocksEdit
        v-if="show"
        :key="renderEdit"
        :blocksData="blocksData.data._rawValue"
        :blockObj="blockObj"
        @updateBlocks="updateBlocks"
      ></BlocksEdit>
    </div>
  </div>
</template>
<script setup lang='ts'>
import { ref } from "vue";

// for getting data from get call
const blocksData = await useAuthLazyFetch(
  "https://v1-orm-lib.mars.hipso.cc/api/blocks/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  {}
);

// Declaring the variables
const renderEdit = ref(0);
const block = ref(blocksData.data._rawValue);
const getData = ref({});
const blockObj = ref({});
const show = ref(false);

// add userprefs fields
const selectedBlocks = ref({
  name: "",
  category: "",
  block_html: null,
  block_css: null,
});

// add the blocks
const addBlocks = async (data: object) => {
  console.log("addddata-------->", data);
  const postPrefs = {
    body: JSON.stringify(data),
  };
  // post call for adding blocks
  useAuthLazyFetchPost(
    "https://v1-orm-lib.mars.hipso.cc/api/blocks/",
    postPrefs
  );
  block.value.unshift(data);
};

// edit the blocks

const prefillData = (data: object) => {
  console.log("upodatedataaaaaaaaa", data);
  show.value = true;
  blockObj.value = data;
  renderEdit.value++;
};
const updateBlocks = async (data: Object) => {
  console.log("deleteDataaaa22222", data);
  const putOptions = {
    body: JSON.stringify(data),
  };
  await useAuthLazyFetchPut(
    `https://v1-orm-lib.mars.hipso.cc/api/blocks/${data.uid}`,
    putOptions
  );
  getCall(data.uid)
};

// delete the blocks
const deleteBlocks = (data: object) => {
  console.log("deleteDataaaa", data);
  const deleteOptions = {
    body: JSON.stringify(data),
  };
  useAuthLazyFetchDelete(
    `https://v1-orm-lib.mars.hipso.cc/api/blocks/${data.uid}`,
    deleteOptions
  );
  getCall(data.uid)
};

// get call through UID
 async function  getCall (data:any){
 await useAuthLazyFetch(`https://v1-orm-lib.mars.hipso.cc/api/blocks/${data}`,{})
}
</script>