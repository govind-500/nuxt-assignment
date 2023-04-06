
<template>
<div>
    <div>
<CollectionList1 :units="units"></CollectionList1>
    </div>
    <div>
 <CollectionAdd1 @add_units="addUnits"></CollectionAdd1>
 <CollectionEdit1 @editUnits="editUnits" :units="units"></CollectionEdit1>
 </div>
 <div>
 </div>
 </div>
</template>
<script lang="ts" setup>


const getOptions = {
  method: "GET",
  headers: {
      "Content-Type": "application/json",
    Authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1IjoiNmZlZDJiYTgwYThkNGM0MjlhZGZiOGQ1ZTZmZTY0ODAiLCJkIjoiMTY4MDA4NCIsInIiOiJzYSIsInAiOiJmcmVlIiwiYSI6ImZpbmRlci5pbyIsImwiOiJ1czEiLCJleHAiOjE2ODMyNzk3Mjl9.5cJkrudAvTWoVRigTNcfQ321W_lOyMm-xsb9rMxuVBE`,
  },
};
var units =  useAuthLazyFetch(
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

function editUnits(data: object)  {
    console.log("data------->",data)
const postOptions = {   
    body: JSON.stringify(data)
  }

    useAuthLazyFetchPut(
    `https://v1-orm-gharpe.mercury.infinity-api.net/api/units/${uid}`,
    postOptions
  );
}


</script>
