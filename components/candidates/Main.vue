<template>
  <div>
    <CandidatesList :cadidateData="getCandidateDate"></CandidatesList>
    <div>
      <CandidatesAdd
        :key="render"
        @add-candidates="addCandidates"
      ></CandidatesAdd>
    </div>
  </div>
</template>
<script setup lang='ts'>
import { Body } from "nuxt/dist/head/runtime/components";
import { ref } from "vue";
const getCandidateDate = ref([]);

// for getting data from get call
const getData = async () => {
  const { data: cadidateData } = await useAuthLazyFetch(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/mock-interviews/?offset=0&limit=100&sort_column=id&sort_direction=desc",
    {}
  );
  getCandidateDate.value = cadidateData.value;
};

// add call for adding the candidates
const addCandidates = async (data: object) => {
  console.log("addDataaaa", data);
  const postCandidate = {
    body: JSON.stringify(data),
  };
  // post call for adding blocks
  await useAuthLazyFetchPost(
    "https://v7-stark-db-orm.mercury.infinity-api.net/api/mock-interviews/",
    postCandidate
  );
  getCandidateDate.value.unshift(data);
  getData();
};
getData();
</script>