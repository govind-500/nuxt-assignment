
<template>
  <div>
    <div>
      <Crud-collectionList
        @search-results="searchUsers"
        :users="users"
        @addUser="addUser"
        @editUser="editUser"
        @deleteUser="deleteUser"
      ></Crud-collectionList>
    </div>
    <div v-if="is_open" :key="addRender">
      <Crud-collectionAdd @saveStorage="saveStorage"></Crud-collectionAdd>
    </div>
    <div v-if="isOpen" :key="editRender">
      <Crud-collectionEdit
        @editSaveStorage="editSaveStorage"
        :users="user"
      ></Crud-collectionEdit>
    </div>
  </div>
</template>
<script lang="ts" setup>

const is_open = ref(false);
const isOpen = ref(false);
const addRender = ref(0);
const editRender = ref(0);
const users = ref([]);
const user = ref({});
const editIndex = ref(0);

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
  users.value.find((item, index) => {
    if (editIndex.value == index) {
      item.name = data.name;
      item.age = data.age;
      item.date_of_birth = data.date_of_birth;
    }
  });
  isOpen.value = false;
  users.value = JSON.parse(data);
  localStorage.setItem("usersList", JSON.stringify(users.value));
};

// delete  user details
const deleteUser = (index: number) => {
  users.value.splice(index, 1);
  localStorage.setItem("usersList", JSON.stringify(users.value));
};

// search results
const searchUsers = (data:string) => {
  console.log("dataaa", data);
 users.value = data
};
</script>
