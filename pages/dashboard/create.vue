<template>
        <div class="project-page">
      <section class="dashboard-header pt-5">
        <div class="container mx-auto relative">
       <Navbar />
        </div>
      </section>
      <section class="container mx-auto pt-8">
        <div class="flex justify-between items-center">
          <div class="w-full mr-6">
            <h2 class="text-4xl text-gray-900 mb-2 font-medium">Dashboard</h2>
          </div>
        </div>
        <div class="flex justify-between items-center">
          <div class="w-3/4 mr-6">
            <h3 class="text-2xl text-gray-900 mb-4">Create New Projects</h3>
          </div>
          <div class="w-1/4 text-right">
          </div>
        </div>
        
        <div class="block mb-2">
          <div class="w-full lg:max-w-full lg:flex mb-4">
            <div
              class="w-full border border-gray-400 bg-white rounded p-8 flex flex-col justify-between leading-normal"
            >
              <form action="" @submit.prevent="createproject" class="w-full">
                <div class="flex flex-wrap -mx-3 mb-6">
                  <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
                    <label
                      class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                    >
                     Name Project
                    </label>
                    <input
                      class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                      type="text"
                      placeholder="Contoh: Metaverse in MultiUniverse"
                      v-model="name_project"
                    />
                  </div>
                  <div class="w-full md:w-1/2 px-3">
                    <label
                      class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                    >
                      Price
                    </label>
                    <input
                    v-model="goal_amount"
                      class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                      type="number"
                      placeholder="Contoh: 200000"
                    />
                  </div>
                  <div class="w-full px-3">
                    <label
                      class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2 mt-3"
                    >
                      Short Description
                    </label>
                    <input
                    v-model="short_description"
                      class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                      type="text"
                      placeholder="Deskripsi singkat mengenai projectmu"
                    />
                  </div>
                  <div class="w-full px-3">
                    <label
                      class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                    >
                      What will backers get
                    </label>
                    <input
                    v-model="feature"
                      class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                      type="text"
                      placeholder="Contoh: 20% dari hasil penjualan"
                    />
                  </div>
                  <div class="w-full px-3">
                    <label
                      class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                    >
                      Description
                    </label>
                    <textarea
                    v-model="description"
                      class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                      type="text"
                      placeholder="Isi deskripsi panjang untuk projectmu"
                    ></textarea>
                  </div>
                   <button type="submit"
              class="bg-green-button hover:bg-green-button text-white font-bold  px-6 py-3 rounded inline-flex items-center"
            >
              Save
            </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </section>
      <div class="cta-clip -mt-20"></div>
      <section class="call-to-action footer-bg pt-64 pb-10"></section>
     <Footer />
    </div>
</template>
<script>
import gql from 'graphql-tag'
export default {
  name: "createpage",
  data(){
    return{
    image:"",
    name_project:"",
    project_leader:"",
    short_description:"",
    backer_count:"",
    current_amount:"",
    feature:"",
    goal_amount:"",
    description:"",
    }
  },
  methods:{
    createproject(event){
      this.$apollo.mutate({
        mutation: gql`
        mutation(
          $name_project: String
          $goal_amount: Int!
          $short_description: String!
          $description: String!
          $feature: String!
        ){
          insert_campagins_one(
    object: {
      name_project: $name_project
      goal_amount: $goal_amount
      description: $description
      short_description: $short_description
      feature: $feature
    }) {
    id
    name_project
    short_description
    goal_amount
    feature
    description
  }
          }`,
          variables:{
             name_project: this.name_project,
    short_description: this.short_description,
    goal_amount: this.goal_amount,
    feature: this.feature,
    description: this.description,
          }
      }).then((data) =>{
        event.target.reset();
        alert("Data anda Masuk")
      })
    }
  }}
</script>