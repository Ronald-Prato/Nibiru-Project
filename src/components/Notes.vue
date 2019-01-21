<template>
  <div class="main_notes_container">
    <div style="display: flex;">
        <h2 style="color: black; margin-right: 2em; padding-top: 3.5%;">Notes *</h2>
        <v-switch v-model="notes_status"/>
    </div>
    
    <div v-if="notes_status">
        <div v-if="notes_status" >
            <div v-if="selected_note == -1">
                <div class="Note" v-for="x in notes_titles" :key="x.id" :id="x.id" @click="open_note">
                    <h3 style="padding: 2% 0 8% 0;"> {{ x.name }} </h3>
                </div>
            </div>
        </div>

        <v-icon color="blue darken-2" class="back_icon" @click="back" v-if="selected_note != -1">exit_to_app</v-icon>

        <v-textarea class="textA" v-if="selected_note == 0" solo :value="notes_content[0]"></v-textarea>
        <v-textarea class="textA" v-if="selected_note == 1" solo :value="notes_content[1]" hint="Complete Customer Info"></v-textarea>
        <v-textarea class="textA" v-if="selected_note == 2" solo :value="notes_content[2]" hint="Complete Customer Info"></v-textarea>
        <v-textarea class="textA" v-if="selected_note == 3" solo :value="notes_content[3]" hint="Complete Customer Info"></v-textarea>    
    </div> 
     
          
          
          
          
          
        <v-alert
        class="temporary_call_score"
        :value="true"
        type="info"
        >
      Estimated call score: 4
    </v-alert>


  </div>
</template>

<script>
export default {
    name: 'Notes',
    data: () => ({
        notes_titles: [
            {name: "Customer service password deleted", id: 0},
            {name: "Debit Card Reissue", id: 1},
            {name: "Address Change", id: 2},
            {name: "Online Banking New Configuration", id: 3},
        ],
        notes_content: [
            "Customer service password was deleted for security reasons",
            "Customer called to request a new debit card because XXX , a new one was sent",
            "Customer called to change the address from XXX to XXX",
            "Customer called because the online banking account was blocked, the customer setted up a new configuration"
        ],

        notes_status: 0,
        selected_note: -1
    }),
    methods: {
        open_note(event) {
            let targetId = event.currentTarget.id;
            this.selected_note = targetId;
        },

        back() {
            this.selected_note = -1;
        }
    }
    
    
}
</script>

<style >
    .main_notes_container {
        width: 96%;
        padding: 2em;
        margin-top: 2em;
        margin-right: 2em;
        background: white;
        box-shadow: 0 10px 6px -6px #777;
        height: 80%;
        position: relative;
    }
    .Note {
        width: 80%;
        height: 20%;
        box-shadow: inset 0 -4px 0 0 steelblue, 0 4px 10px -2px #777;
        margin-bottom: 1em;
        padding: 1em;
    }
    .Note:hover {
        cursor: pointer;
    }
    .back_icon {
        transform: scaleX(-1); 
        font-size: 3em; 
        position: absolute;
        right: 5%;
        top: 5%;
        color: steelblue;
    }
    .back_icon:hover {
        cursor: pointer;
    }
    .textA {
        font-size: 1.2em;
    }
    .temporary_call_score {
        position: absolute;
        bottom: -10.4em;
        left: 0;
        width: 100%;
        height: 18%;
        font-size: 1em;
    }
</style>
