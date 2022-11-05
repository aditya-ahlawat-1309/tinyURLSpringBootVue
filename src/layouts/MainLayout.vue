<template>
  <q-layout view="lHh Lpr lFf" >
    <div style="background-color:white; opacity:0.15;box-shadow: 10px 10px 15px 100px  #ff0080;width:40%;height:90%;position:absolute;z-index:0"></div>
    <br/>
    <div style="margin-left:5%">
    <h4>tinyURL</h4>
    <h5>Kindly Enter the Alias and the URL</h5>
    <div class="q-pa-md" style="max-width: 400px">

      <q-form class="q-gutter-md">
        <h5>Alias</h5>
        <input
          placeholder="&nbsp;&nbsp; Enter Alias"
          v-model="form.alias"
          required
          style="margin-top:-10%;border:none; height:65px;width:85%;background-color:#f3f3e3;border-radius:20px;color:black"
        />
        
        <h5>URL</h5>
        <input
          placeholder=" &nbsp;&nbsp; Enter Url Name"
          v-model="form.url"
          required
          style="margin-top:-10%;border:none; height:65px;width:85%;background-color:#f3f3e3;border-radius:20px;color:black"
        />
        <br/>
        <br/>
        <q-btn
          @click="onSubmit()"
          style="background: #ff0080; color: white"
          label="generate"
        />
      </q-form>


<h6><a :href="`https://tiny-url-youtube.herokuapp.com/${(linkAlias ? linkAlias.alias : '')}`">Generated URL</a> </h6>


    </div>
  </div>
    <q-page-container>
     
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent} from 'vue'
import { useQuasar } from 'quasar'
import { ref } from 'vue'
import axios from 'axios'

export default defineComponent({
  name: 'MainLayout',

  components: {},
  data(){
        return {
              
                }
            },



  setup () {
    const $q = useQuasar()
    const linkAlias = ref([])
    const name = ref(null)
    const age = ref(null)
    const accept = ref(false)

    return {
      name,
      age,
      accept,
      form:{
        alias:"",
        url:"",
      },
      linkAlias,
    
       
  onSubmit() {

        axios.post("https://tiny-url-youtube.herokuapp.com/",this.form)
        .then((response) => {
          linkAlias.value = response.data
          console.log(linkAlias.value.alias);
        } )
        .catch(err => console.log(err))
      }
    }
  }
})
</script>
