<template>
	<div class="section section--login">
    <h1>{{ character.name }}</h1>
    <h2>Edit your information in CRI</h2>
		<p class="small small--dimmed">Citizen ranking initiative is powered by Anni Corp. Anni Corp does not accept any liability directly or indirectly caused by its action or inaction. All modifications will be logged.</p>
		<!-- <characterform @createOrUpdate="createOrUpdate" :character=this.character></characterform> -->
		<characterform @createOrUpdate="createOrUpdate" :character="character"></characterform>
	</div>
</template>
  

<script>
import CharacterForm from '../../components/CharacterForm.vue';
export default {
  name: 'Character',
  components: {
    'characterform': CharacterForm
  },
  data: function() {
    return {
      character: {}
    };
  },
  methods: {
    getOneCharacterData: function() {
      console.log("getOneCharacterData fired."); 
      //fetch('/api/get_character', {method: 'GET'})
	  fetch(`/api/get_character?char=${this.$route.params.id}`, {method: 'GET'})
      .then((response) => response.json())
      .then(response => { 
		this.character = response;
		//console.log(response);
      })    
      .catch((errors) => {    
        console.log("Could not get ONE character");
        //console.log(errors);
        this.$router.push('/dashboard'); 
      })    
    },
    createOrUpdate: async function(character) {
		fetch('/api/edit', {method: 'POST', headers: {"Content-Type": "application/json"}, body: JSON.stringify(character)})
    }
  },
  mounted() {    
		this.getOneCharacterData()
	}
};
</script>