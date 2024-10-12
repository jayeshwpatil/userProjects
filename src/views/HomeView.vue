<script setup>
import { computed, onBeforeMount, ref, watch } from 'vue'
import viewProject from '@/components/viewProject.vue'
const props = defineProps(["dummyData"])
const finalData = ref(props.dummyData)
const viewProjectData = ref([])
const SearchUser = ref(null)
let sortChoose = ref("asc"); // default sorting order

const userCount = computed(() => {
  return finalData.value.length
})
const viewProjects = (data) => {
  //console.log("id is ", data)
  // viewProjectData.value.push(data)
  viewProjectData.value = finalData.value.filter((item) => item.id === data.id)
  console.log("viewProject is ", viewProjectData.value)
}

// const searchResult = () => {
//   finalData.value = finalData.value.filter((item) => item.fullName == SearchUser.value)
// }

watch(SearchUser, (newVal) => {
  if (newVal) {
    finalData.value = props.dummyData.filter((item) => item.fullName.toLowerCase().includes(newVal.toLowerCase()))
  }
  else {
    finalData.value = props.dummyData
  }
})



const finalOutput = computed(() => {
  if (sortChoose.value === "asc") {
    console.log("asc")
    return finalData.value.sort((a, b) => a.fullName.localeCompare(b.fullName))
  } else if (sortChoose.value === "des") {
    console.log("dsc")
    return finalData.value.sort((a, b) => b.fullName.localeCompare(a.fullName))
  } else {
    console.log("nothing")
    return finalData.value
  }
})





</script>

<template>
  <div class="container my-5 ">
    <div class="row ">
      <div class="col-sm-6 border border-success bg-warning">
        <h1 class="SectionTitle">Active Users </h1>
        <div class="mb-3">
          <input class="form-control border-success border-2" placeholder="SearchUser" v-model="SearchUser">
        </div>
        <div class="d-flex justify-content-between">
          <p> <span class="badge text-bg-success">{{ userCount }}</span> Users Found</p>
          <div class="mb-3">
            <select class="form-select fw-bold border-dark border-1" v-model="sortChoose">
              <option value="asc">Sort By Ascending </option>
              <option value="des">Sort By Descending </option>
            </select>
          </div>
        </div>
        <div class="overflowBox mb-3">
          <ul class="lists" v-for="(item, index) in finalOutput" :key="index">
            <li class="d-flex justify-content-between align-items-center">
              <div>
                <p class="fw-bold text-dark p-0 m-0 pointer" @click="viewProjects(item)">{{ item.fullName }}</p>
                <p class="pointer" @click="viewProjects(item)"> <i class="bi bi-arrow-return-right mx-2"></i> <strong
                    class="text-danger">{{ item.projects.length
                    }}</strong> Project </p>
              </div>
              <a href="#ProjectNames" class="btn btn btn-success" @click.prevent="viewProjects(item)"> View Projects
                <i class="bi bi-arrow-right-circle"></i></a>
            </li>
          </ul>
        </div>
      </div>
      <div class="col-sm-6 bg-dark " id="ProjectNames" style="min-height: 250px;">
        <viewProject :viewingProjectData="viewProjectData"></viewProject>
      </div>
    </div>

  </div>

</template>

<style>
.pointer {
  cursor: pointer
}

a {
  text-decoration: none;
}

.SectionTitle {
  font-size: 25px;
  font-weight: bold;
  padding: 20px 0px;
}

.overflowBox {
  overflow: auto;
  height: 400px;
  padding-right: 10px;
}

.lists {
  margin: 0px;
  padding: 0px;
  display: block;
}

.lists li {
  border: 1px solid #000;
  margin-bottom: 18px;
  display: block;
  background: #fff;
  padding: 10px 15px;
}

@media only screen and (max-width: 768px) {
  .overflowBox {
    height: 250px !important;
  }

  .container.my-5 {
    margin-top: 0px !important;
    margin-bottom: 0px !important;
  }
}

/* Custom scrollbar for WebKit browsers */
::-webkit-scrollbar {
  width: 4px;
  /* Width of the scrollbar */
}

::-webkit-scrollbar-track {
  background: #f6f0c1;
  /* Background of the scrollbar track */
}

::-webkit-scrollbar-thumb {
  background: #000;
  /* Color of the scrollbar thumb */
  border-radius: 4px;
  /* Rounded corners */
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
  /* Color when hovered */
}
</style>