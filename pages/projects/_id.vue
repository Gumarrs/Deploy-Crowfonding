<template>
<ApolloQuery :query="require('../../graphql/detail.gql')" :variables="{id: CampaignId}">
<template v-slot="{ result: { loading, data } }">
  <div v-if="loading" class="loading apollo">Loading...</div>
  <div v-else-if="data" class="result apollo">
     <div class="project-page">
      <section class="project-header pt-5">
        <div class="container mx-auto relative">
     <Navbar />
        </div>
      </section>
      <section class="container project-container mx-auto -mt-56">
        <div class="flex mt-3">
          <div class="w-3/4 mr-6">
            <div class="bg-white p-3 mb-3 border border-gray-400 rounded-20">
              <figure class="item-image">
                <img
                  :src="`${data.campagins_by_pk.image}`"
                  alt=""
                  class="rounded-20 w-full"
                />
              </figure>
            </div>
          </div>
          <div class="w-1/4">
            <div
              class="bg-white w-full p-5 border border-gray-400 rounded-20 sticky"
              style="top: 15px"
            >
              <h3>Project Leader:</h3>

              <div class="flex mt-3">
                <div class="w-1/4">
                  <img :src="`${data.campagins_by_pk.foto_profil}`"
              
                    alt=""
                    class="w-full inline-block rounded-full"
                  />
                </div>
                <div class="w-3/4 ml-5 mt-1">
                  <div class="font-semibold text-xl text-gray-800">
                    {{data.campagins_by_pk.project_leader}}
                  </div>
                  <div class="font-light text-md text-gray-400">
                    {{data.campagins_by_pk.backer_count}} Backer
                  </div>
                </div>
              </div>

              <h4 class="mt-5 font-semibold">What will you get:</h4>
              <ul class="list-check mt-3">
              <li >
                {{data.campagins_by_pk.feature}}
              </li>
              </ul>
              <input
                type="number"
                class="border border-gray-500 block w-full px-6 py-3 mt-4 rounded-full text-gray-800 transition duration-300 ease-in-out focus:outline-none focus:shadow-outline"
                placeholder="Amount in Rp"
                value=""
              />
              <a
                href="https://www.shareaholic.com/api/share/?v=1&apitype=1&apikey=8943b7fd64cd8b1770ff5affa9a9437b&service=whatsapp&title=Chat%20admin&link=www.google.com"
                class="text-center mt-3 button-cta block w-full bg-orange-button hover:bg-green-button text-white font-medium px-6 py-3 text-md rounded-full"
              >
                Fund Now
              </a>
            </div>
          </div>
        </div>
      </section>
      <section class="container mx-auto pt-8">
        <div class="flex justify-between items-center">
          <div class="w-full md:w-3/4 mr-6">
            <h2 class="text-4xl text-gray-900 mb-2 font-medium">
              {{data.campagins_by_pk.name_project}}
            </h2>
            <p class="font-light text-xl mb-5">
              {{data.campagins_by_pk.short_description}}
            </p>

            <div class="relative progress-bar">
              <div
                class="overflow-hidden mb-4 text-xs flex rounded-full bg-gray-200 h-6"
              >
                <div
                    :style="'width: ' + (data.campagins_by_pk.current_amount / data.campagins_by_pk.goal_amount) * 100 + '%'"
                  class="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-purple-progress progress-striped"
                ></div>
              </div>
            </div>
            <div class="flex progress-info mb-6">
              <div class="text-2xl">{{(data.campagins_by_pk.current_amount / data.campagins_by_pk.goal_amount) * 100}}%</div>
              <div class="ml-auto font-semibold text-2xl">Rp {{ new Intl.NumberFormat().format(data.campagins_by_pk.goal_amount) }}</div>
            </div>

            <p class="font-light text-xl mb-5">
            {{data.campagins_by_pk.description}}
            </p>
              <p class="font-light text-xl mb-5">
              If Your Interest Call {{data.campagins_by_pk.contact}}
            </p>
         
          </div>
          <div class="w-1/4 hidden md:block"></div>
        </div>
      </section>
      <div class="cta-clip -mt-20">
        <h1> </h1>
      </div>
<CallToAction />
 <Footer />
    </div>   
  </div>
    </template>
</ApolloQuery>
</template>

<script>
export default {
  name : "DetailPage",
 computed:{
   CampaignId(){
     return this.$route.params.id;
   }
 }
}
</script>