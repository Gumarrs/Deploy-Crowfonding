<template>
<ApolloQuery :query="require('../../../graphql/detail.gql')" :variables="{id: CampaignId}">
<template v-slot="{ result: { loading, data } }">
  <div v-if="loading" class="loading apollo">Loading...</div>
    <div v-else-if="data" class="result apollo">
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
            <h3 class="text-2xl text-gray-900 mb-4">Campaign Details</h3>
          </div>
          <div class="w-1/4 text-right">
            <nuxt-link
              to="/dashboard/projects/create"
              class="bg-green-button hover:bg-green-button text-white font-bold px-4 py-1 rounded inline-flex items-center"
            >
              Edit
            </nuxt-link>
          </div>
        </div>
        <div class="block mb-2">
          <div class="w-full lg:max-w-full lg:flex mb-4">
            <div
              class="border border-gray-400 bg-white rounded p-8 flex flex-col justify-between leading-normal"
            >
              <div>
                <div class="text-gray-900 font-bold text-xl mb-2">
                  {{name_project}}
                </div>
                <p class="text-sm font-bold flex items-center mb-1">
                  Description
                </p>
                <p class="text-gray-700 text-base">
                 {{data.campagins_by_pk.description}}
                </p>
                <p class="text-sm font-bold flex items-center mb-1 mt-4">
                  Price
                </p>
                <p class="text-4xl text-gray-700 text-base">{{data.campagins_by_pk.goal_amount}}</p>
              </div>
            </div>
          </div>
        </div>
      </section>
      <div class="cta-clip -mt-20"></div>
      <section class="call-to-action footer-bg pt-64 pb-10"></section>
     <Footer />
        </div>
    </div>
</template>
</ApolloQuery>
</template>
<script>
export default {
    name : "DetailPage1",
 computed:{
   CampaignId(){
     return this.$route.params.id;
   }
 }
}
</script>