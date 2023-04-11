
<template>
  <div>
    <div>
      <CrudList
        :users="users"
        @addUser="addUser"
        @editUser="editUser"
        @deleteUser="deleteUser"
      ></CrudList>
    </div>
    <div v-if="is_open" :key="addRender">
      <CrudAdd @saveStorage="saveStorage"></CrudAdd>
    </div>
    <div v-if="isOpen" :key="editRender">
      <CrudEdit @editSaveStorage="editSaveStorage" :users="user"></CrudEdit>
    </div>
  </div>
</template>
<script lang="ts" setup>
import { ref, onMounted } from "vue";

// Declaring the varibles
const is_open = ref(false);
const isOpen = ref(false);
const addRender = ref(0);
const editRender = ref(0);
const users = ref([]);
const user = ref({});
const editIndex=ref(0)

onMounted(() => {
  const userList = localStorage.getItem("usersList");
  users.value = JSON.parse(userList);
  console.log("this.hello", users.value);
});

// open add user modal
const addUser = () => {
  is_open.value = true;
  addRender.value++;
};

// open edit user modal
const editUser = (data: any) => {
  user.value = { ...data };
  isOpen.value = true;
  editRender.value++;
};

// save add user details
const saveStorage = (data: object) => {
  users.value.push(data);
  localStorage.setItem("usersList", JSON.stringify(users.value));
  is_open.value = false;
};
// edit add user details
const editSaveStorage = (data: any) => {
users.value.find((item,index)=>{
if(editIndex.value==index){
item.name= data.name
item.age=data.age
item.date_of_birth=data.date_of_birth
}
})
  isOpen.value = false;
  users.value = JSON.parse(data);
  localStorage.setItem("usersList", JSON.stringify(users.value));

};

// delete  user details
const deleteUser = (index: number) => {
  users.value.splice(index,1);
  localStorage.setItem("usersList", JSON.stringify(users.value));
};
</script>
