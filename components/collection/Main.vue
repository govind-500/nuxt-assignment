
<template>
<div>
    <div>
<CollectionList1 :units="units" @editUnits="editUnits"></CollectionList1>
    </div>
    <div>
 <CollectionAdd1 @add_units="addUnits"></CollectionAdd1>
 <CollectionEdit1 v-if="show" @editUnits="editUnits" :units="unitObj"></CollectionEdit1>
 </div>
 <div>
 </div>
 </div>
</template>
<script lang="ts" setup>
const show = ref(false)
const unitObj = ref({})
const getOptions = {
  method: "GET",
  headers: {
      "Content-Type": "application/json",
    Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNmZlZDJiYTgwYThkNGM0MjlhZGZiOGQ1ZTZmZTY0ODAiLCJkIjoiMTY4MDA4NCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzk3Mjl9.5cJkrudAvTWoVRigTNcfQ321W_lOyMm-xsb9rMxuVBE`,
  },
};
var units = await useAuthLazyFetch(
     " https://v1-orm-gharpe.mercury.infinity-api.net/api/units/?offset=0&limit=100&sort_column=id&sort_direction=desc",
  getOptions
);
console.log("units444444444444",units)


// Add Template to the template data
function addUnits(data: object)  {
    console.log("data------->",data)
const postOptions = {   
    body: JSON.stringify(data)
  }

    useAuthLazyFetchPost(
    "https://v1-orm-gharpe.mercury.infinity-api.net/api/units/",
    postOptions
  );
}
function deletUnits(data: object)  {
    console.log("data------->",data)
const postOptions = {   
    body: JSON.stringify(data)
  }

    useAuthLazyFetchDelete(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/units/${uid}`,
    postOptions
  );
}

 const editUnits = (data: object) => {
   show.value = true
   unitObj.value = data;
   

}

</script>
