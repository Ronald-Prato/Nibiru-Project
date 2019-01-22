<template>
    <div>
        <div class="main_notes_container">
  
        
            <div class="Note_Header">
                <div style="display: flex; align-items: center; justify-content: space-around;">
                    <h2 style="color: black; margin: 0 2em .3em 7em;">Notes *</h2>
                    <v-switch v-model="notes_status" />
                </div>
            </div>

            <div class="Note_Container">
                <div v-if="notes_status">
                    <div v-if="notes_status" >
                        <div v-if="selected_note == -1">
                            <div class="Note" v-for="x in notes_data" :key="x.id" :id="x.id" @click="open_note">
                                <h3 style="padding: 2% 0 8% 0;"> {{ x.name }} </h3>
                            </div>
                        </div>
                    </div>

                    <v-icon color="blue darken-2" class="back_icon" @click="back" v-if="selected_note != -1">exit_to_app</v-icon>

                    <div v-for="x in notes_data" :key="x.id">
                        <v-textarea 
                        class="textA" 
                        v-if="selected_note == x.id" 
                        solo :value="notes_content[x.id]" 
                        hint="Complete the information in CAPITAL_LETTERS if necessary">
                        </v-textarea>
                    </div>
 
                </div> 
            </div>
          
          
        </div>    
        
    </div>
</template>

<script>
export default {
    name: 'Notes',
    data: () => ({
        notes_data: [
            {name: "Customer service password deleted", id: 0},
            {name: "Debit Card Reissue", id: 1},
            {name: "Address Change", id: 2},
            {name: "Online Banking New Configuration", id: 3},
            {name: "Travel notification", id: 4},
            {name: "NSF Not eligible account", id: 5},
            {name: "Disputes", id: 6},
            {name: "Closing Account", id: 7},
            {name: "Limmit Increase", id: 8}
        ],
        notes_content: [
            "Customer service password was deleted for security reasons",
            "Customer called to request a new debit card because XXX , a new one was sent",
            "Customer called to change the address, verified old one and provided new one: NEW_ADDRESS",
            "Customer called because the online banking account was blocked, the customer setted up a new configuration",
            "Travel Notification Submited, from START_DATE to END_DATE, destination: TRAVEL_PLACE",
            "The customer was told that his account is not eligible for fee reversals anymore",
            "Customer called requesting a disputes for REASON_OF_THE_DISPUTE",
            "Customer called for closing the account because CLOSING_REASON",
            "Customer called to request a limit increase on the debit card for ATM_OR_POS, from INITIAL_AMOUNT to REQUESTED_AMOUNT, the account WAS_WASNT eligible for the increase"
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
    :root {
        --main-pad: 2em;     
    }
    .main_notes_container {
        width: 96%;
        padding: var(--main-pad);
        margin-top: var(--main-pad);
        margin-right: var(--main-pad);
        background: white;
        box-shadow: 0 10px 6px -6px #777;
        height: 96.6%;
        position: relative;
        overflow: auto;
    }
    .Note_Container {
       position: absolute;
       width: 90%;
       padding-top: 20%;
    }
    .Note_Header {
        position: fixed;
        margin-top: -2em;
        margin-left: -2em;
        padding: 1%;
        width: 26.65%;
        z-index: 1;
        background: white;
        box-shadow:  inset 0 8px 0 0 steelblue, 0 5px 10px -.5px #777;
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
        z-index: 1;
    }
    .back_icon:hover {
        cursor: pointer;
    }
    .textA {
        font-size: 1.2em;
    }
</style>
