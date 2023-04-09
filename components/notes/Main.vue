<template>
  <div>
    <div>
      <NotesList
        :noteBody="noteBody"
        @showAdd="showAdd"
        @edit="showEdit"
        @deleteProject="deleteNotes"
      />
    </div>
    <div v-if="open">
      <NotesAdd @addNote="addNotes" :key="addRender" />
    </div>
    <div v-if="showEditModal">
      <NotesEdit
        @editNote="editProject"
        :updateNote="updateNote"
        :key="editRender"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

// Declaring the variables
const open = ref(false)
const addRender = ref(0)
const editRender = ref(0)
const showEditModal = ref(false)
const updateNote = ref({})
const noteBody = ref([])
let projectId = ref('')
const { data: notesData } = useAuthLazyFetch(
  `https://v1-orm-lib.mars.hipso.cc/api/notes/CONTACTS/string?project_id=12&offset=0&limit=100&sort_column=id&sort_direction=desc`,
  {}
)
noteBody.value = notesData.value

// add slidebar
const showAdd = (data:any) => {
  open.value = data
  addRender.value++
}
// open edit slidebar
const showEdit = (data:any) => {
  showEditModal.value = true
  editRender.value++
  updateNote.value = data
}

// add the notes
const addNotes = async (body: Object) => {
  const postOptions = {
    body: body,
  }
  await useAuthLazyFetchPost(
    'https://v1-orm-lib.mars.hipso.cc/api/notes/CONTACTS/string',
    postOptions,
  )
  noteBody.value.unshift(body)
}

// edit the notes
const editProject = async (body: object) => {
  const putOptions = {
    body: body,
  }
  await useAuthLazyFetchPut(
    `https://v1-orm-lib.mars.hipso.cc/api/notes/${body.uid}`,
    putOptions,
  )
  const { data: response } = await useAuthLazyFetch(
    'https://v1-orm-lib.mars.hipso.cc/api/notes/CONTACTS/string?project_id=12&offset=0&limit=100&sort_column=id&sort_direction=desc',
    {}
  )
  noteBody.value = response.value
}
// delete the notes
const deleteNotes = async (data: object, index:number) => {
  await useAuthLazyFetchDelete(
    `https://v1-orm-lib.mars.hipso.cc/api/notes/${data.uid}`,
    {}
  )
  noteBody.value.splice(index, 1)
}
</script>