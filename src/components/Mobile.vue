<template>
  <div class="main_mobile_container">
    <h2 style="color: steelblue;">Mobile Authenticated  | M |</h2>
    
    <v-container fluid >
        <div class="call_features">
            <h3 class="feature_item" >Opening with the bank name and your name *</h3>
            <h3 class="feature_item" >Ask for the customer's name *</h3>
            <h3 class="feature_item" >Aknowledge Statement (Try to repeat the customer's problem) *</h3>
            <v-expansion-panel style="">
                <v-expansion-panel-content style="box-shadow: 0 1px 0 0 rgb(209, 209, 209);" >
                    <div slot="header" class="transfer">Verification (Customer is already in Level 1)</div>
                    <v-card style="height: 21em;">
                        <v-card-text style="color: steelblue; padding-bottom: 0;" v-if="!verificated">Ask just one for level 2</v-card-text>
                        <v-card-text style="color: green; padding-bottom: 0;" v-else>Customer on Level 2</v-card-text>
                        <v-radio-group v-model="verificated" style="padding: 1em;">
                            <v-radio style="margin-bottom: 0;" label="Customer Service Pasword" value="1" />
                            <span style="font-size: 12px; margin-left: 12%; width: 100%; color: tomato; margin-bottom: 1.5em;">
                                Delete it if customer doesn't remember it or if is the last 4 of social
                            </span>
                            <v-radio style="margin-bottom: 1.5em;" label="Amount of the last deposit" value="2"/>
                            <v-radio style="margin-bottom: 0;" label="Name of Joint Owners" value="3" />
                            <span style="font-size: 12px; margin-left: 12%; width: 100%; color: steelblue; margin-bottom: 1.5em;">
                                Ask only if customer has Joint Owners <span style="color: tomato; text-decoration: underline;">NOT</span> "Beneficiary"
                            </span>
                            <v-radio style="margin-bottom: 0;" label="Amount of the last ACH" value="4" />
                            <span style="font-size: 12px; margin-left: 12%; width: 100%; color: steelblue; margin-bottom: 1.5em;">
                                Automatic credits and debits in the account
                            </span>
                        </v-radio-group>
                    </v-card>   
                    
                    
                </v-expansion-panel-content>
            </v-expansion-panel>
            <h3 class="feature_item" >Self Service Options (not if is just offering the app) *</h3>
            <v-expansion-panel>
                <v-expansion-panel-content style="box-shadow: 0 1px 0 0 rgb(209, 209, 209);" >
                    <div slot="header" class="transfer">Transfer the Call</div>
                    <v-card style="height: 24em;">
                        <Transfer />
                    </v-card>   
                    
                    
                </v-expansion-panel-content>
            </v-expansion-panel>
            <h3 class="feature_item" >Further Assistance *</h3>
            <h3 class="feature_item" >Offer the Survey</h3>
            <h3 class="feature_item" >Closing with the name of the Branch *</h3>
            
        </div>
        <div class="boolean_options">
            <v-switch id="switch_item" class="boolean_item" v-model="g"/>
            <v-switch id="switch_item" class="boolean_item" v-model="f"/>
            <v-switch id="switch_item" class="boolean_item" v-model="e"/>
            <v-switch id="switch_item" class="boolean_item" v-model="verificated"/>
            <v-switch id="switch_item" class="boolean_item" v-model="d"/>
            <v-switch id="switch_item" class="boolean_item" v-model="sub_transfered"/>
            <v-switch id="switch_item" class="boolean_item" v-model="c"/>
            <v-switch id="switch_item" class="boolean_item" v-model="b"/>
            <v-switch id="switch_item" class="boolean_item" v-model="a"/>
            
            
        </div>

        <div v-if="sub_transfered" class="Transfer_Confirmation">
            <p style="text-align: center; color: white; background: steelblue; width: 100%; ">
                ¿Did you give the deparment's number to the customer?</p> <br/>
            <v-radio-group v-model="transfered" style="position: relative; position: absolute;  right: 0; top: 20%;">
                <v-radio label="Yes" value="1" style="position: absolute; right: 7em; top: 1em;"></v-radio>
                <v-radio label="No, Justified Reasons" value="0" style="position: absolute; right: 4.6em; top: 4em;"></v-radio>
                
            </v-radio-group>
            
        </div>
    </v-container>
    
    <div class="Hold_Tracker">
        <p style="position: absolute; left: 6.5%; top: 15%; color: black; font-weight: bolder">Hold Tracker</p>
        <v-btn color="info" @click="timer_count" :disabled="disable_button">Start</v-btn>
        <v-btn color="error" @click="reset_timer">Reset</v-btn>
        <v-progress-circular
        :rotate="90"
        :size="80"
        :width="15"
        :value="value"
        color="teal"
        >
            {{ minute }}:{{ seconds }}
        </v-progress-circular>
    </div>
    <v-btn 
            color="info" 
            @click="refresh_values"
            style="position: absolute; top: 50%; right: 2.8%;"
            
        >Reset</v-btn>

  </div>
</template>

<script>
import Transfer from './Transfer';
var count;
export default {
    name: 'Mobile',
    components: {
        Transfer
    },
    data: () => ({
        disable_button: false,

        verificated: 0,
        sub_transfered: 0,
        transfered: 0,
        value: 120,
        minute: 2,
        seconds: '00',

        a: 0, b: 0, c: 0, d: 0, e: 0, f: 0, g: 0
    }),
    methods: {
        
        timer_count() {
            var sound = 'http://soundbible.com/mp3/Tick Tock-SoundBible.com-1165545065.mp3';
            var playSound = new Audio(sound);
            if (!this.value) {
                this.value = 120;
                this.minute = 2;
                this.seconds = '00';
                playSound.pause();
            }
            this.disable_button = true;
            
            
            count = setInterval( () => {
                if (this.seconds == '00') {
                    this.seconds = 60;
                }
                this.value --;
                this.seconds --;
                this.seconds == 59 ? this.minute -- : this.minute
                

                if (this.minute == 0 && this.seconds == 0) {
                    this.value = 0;
                    this.seconds = '0';
                    this.minute = 0;
                    clearInterval(count);
                }
           
                
                if (this.seconds < 10) {
                    this.seconds = '0'+this.seconds;
                }


                if (this.value == 20 || this.value == 10) {
                    playSound.play();
                }else if(this.value == 0) {
                    clearInterval(count);
                    this.disable_button = false;
                    
                }
            }, 1000);
        },

        reset_timer() {
           
            this.value = 120;
            this.minute = 2;
            this.seconds = '00';
            clearInterval(count);
            this.disable_button = false;
            playSound.pause();
        },
        refresh_values () {
            this.a = 0; 
            this.b = 0; 
            this.c = 0; 
            this.d = 0; 
            this.e = 0; 
            this.f = 0; 
            this.g = 0;
            this.verificated = 0;
            this.sub_transfered = 0;
        }
    }
}
</script>

<style >
    .main_mobile_container {
        padding: 1em;
        margin-top: 2em;
        background: white;
        box-shadow: 0 10px 6px -6px #777;
        height: 96.6%;
        position: relative;
    }
    .call_features {
        width: 60%;
    }
    .feature_item {
        flex: auto;
        margin: 0;
        padding-left: 1em;
        background: rgba(255, 255, 255, .5);
        width: 100%;
        line-height: 4.15em;
        box-shadow: 0 4px 6px -2px #777;
        border-bottom: .2px solid rgb(209, 209, 209);
    }
    .feature_item:not(:first-child):not(:last-child) {
        border-top: none;
        
    }
    .feature_item:last-child {
        border-top: none;
    }
    .boolean_options {
        position: absolute;
        top: calc(5em - 5px);
        right: 33%;
        width: 5em;
        display: flex;
        flex-direction: column;
        align-items: center;
        box-shadow: 0 2px 3px -2px #777;
    }
    .boolean_item:not(:last-child) {
        box-shadow: 0 1px 0 0 rgb(209, 209, 209);
    }
    .transfer {
        flex: auto;
        margin-left: -6px;
        line-height: 2.6em;
        font-size: 1.21em;
        font-weight: bold;
    }
    .Transfer_Confirmation {
        width: 25%;
        height: 25%;
        position: relative;
        position: absolute;
        right: 1%;
        top: 1%;
        padding: 1em;
        box-shadow: 0 10px 6px -6px #777;
        border: .5px solid #e0e0e0;
    }
    .Transfer_Options {
        display: flex;
        flex-direction: column;
        justify-content: space-around;
    }
    .Transfer_Options2 {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .Hold_Tracker {
        position: relative;
        position: absolute;
        right: 1%;
        bottom: 1%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        box-shadow: 0 4px 6px -2px #777;
        padding: 1em;
        padding-top: 2em;
    }
</style>
