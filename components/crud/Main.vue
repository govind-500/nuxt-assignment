
<template>
  <div>
    <div>
      <CrudList :users="users" @addUser="addUser" @editUser="editUser" @deleteUser="deleteUser"></CrudList>
    </div>
    <div v-if="is_open" :key="addRender">
      <CrudAdd @saveStorage="saveStorage"></CrudAdd>
    </div>
    <div v-if="isOpen">
        <CrudEdit @editSaveStorage="editSaveStorage" :users="user"></CrudEdit>
    </div>
  </div>
</template>
<script lang="ts" setup>
import { ref,onMounted } from "vue";

const is_open = ref(false);
const isOpen = ref(false);
const addRender = ref(0);
const editRender=ref(0)
const users = ref([]);
const user = ref({});

onMounted(() => {
  const userList = localStorage.getItem("usersList");
  users.value = JSON.parse(userList);
  console.log("this.hello", users.value);
});

const addUser = () => {
  is_open.value = true;
  addRender.value++;
};
const editUser=(data:any)=>{
    console.log("dataaaaqa",data)
      user.value = { ...data };
     isOpen.value = true;
  editRender.value++;
}

const saveStorage = (data: object) => {
  console.log("dataaaaaaa", data);
  users.value.push(data);
  localStorage.setItem("usersList", JSON.stringify(users.value));
  console.log("userssssss", users.value);
  is_open.value = false;
};

const editSaveStorage =(data:any)=>{
  console.log("data",data);
  
    users.value= JSON.parse(data);
  
  localStorage.setItem("usersList", JSON.stringify(users.value));
}

const deleteUser=(index:number)=>{
    users.value.splice(index,1)
    localStorage.setItem("usersList", JSON.stringify(users.value));
}

</script>
