<template>
  <div class="main_mobile_container">
    <h2 style="color: steelblue;">No Customer Info | N |</h2>
    
    <v-container fluid >
        <div class="call_features">
            <h3 class="feature_item" >Opening with the bank name *</h3>
            <h3 class="feature_item" >Ask for the customer's name *</h3>
            <h3 class="feature_item" >Aknowledge Statement (Try to repeat the customer's problem) *</h3>

            

            <v-expansion-panel>
                <v-expansion-panel-content style="box-shadow: 0 1px 0 0 rgb(209, 209, 209);" >
                    <div style="padding: 6%; padding-top: 0; padding-bottom: 8%;">
                        <v-autocomplete
                        :items="pull_on_method"
                        :filter="customFilter"
                        color="blue"
                        item-text="name"
                        label="Input Method"
                        autofocus
                        light
                        v-model="method"
                    ></v-autocomplete>
                    </div>

                    
                    
                    <div slot="header" class="transfer">Verification</div>
                        <div v-if="method != ''">
                            <div v-if="method == 'Account Number'"> <!-- Account Number -->
                                <v-card style="height: 36em; padding: 5%; padding-top: 0;">
                                    <v-card-text v-if="verificated < 2" style="color: steelblue; padding-bottom: 0;">
                                        Ask two questions for level 1
                                    </v-card-text>
                                    <v-card-text v-else-if="verificated == 2" style="color: green; padding-bottom: 0;">
                                        Customer is level 1. Ask 1 question more for level 2 
                                    </v-card-text>
                                    <v-card-text v-else-if="verificated == 3" style="color: green; padding-bottom: 0;">
                                        Customer is level 2
                                    </v-card-text>
                                
                                    <div style="padding: 1em;" >
                                        <v-checkbox style="height: 1.5em;" label="Customer Service Pasword" @change="check_verification" v-model="CSP" />
                                        <span v-if="!CSP" style="font-size: 12px; margin-left: 6.8%; width: 100%; color: tomato;">
                                            Don't ask it if are the last 4 of social. Delete it if customer doesn't remember it
                                        </span>
                                        

                                        <v-radio-group v-model="SSN_DLN" style="margin-top: 2em;" @change="check_verification">
                                            <v-radio style="margin-bottom: 10%;" label="Social Security Number" value="1" />
                                            <v-radio style="margin-bottom: 0;" label="Drivers License Number" value="2" />
                                            <!--Restar 1 al final-->
                                        </v-radio-group>
                                        


                                        <v-checkbox style="height: 1.5em;" label="Name of Joint Owners" v-model="JO" @change="check_verification"/>
                                        <span v-if="!JO" style="font-size: 12px; margin-left: 6.8%; width: 100%; color: steelblue; margin-bottom: 1.5em;">
                                            Ask only if customer has Joint Owners <span style="color: tomato; text-decoration: underline;">NOT</span> "Beneficiary"
                                        </span>

                                        <v-checkbox label="Amount of the Deposit" v-model="LD" @change="check_verification"/>

                                        <v-checkbox style="height: 1.5em;" label="Amount of the last ACH" v-model="ACH" @change="check_verification"/>
                                        <span style="font-size: 12px; margin-left: 6.8%; width: 100%; color: steelblue; margin-bottom: 1.5em;">
                                            Automatic credits and debits in the account
                                        </span>
                                        <v-checkbox label="Amount of the Check Cleared" v-model="CC" @change="check_verification"/>
                                        
                                        
                                    </div>
                                </v-card>
                            </div>

                            <div v-if="method == 'Social Security Number'">  <!-- Social Security Number -->
                                <v-card style="height: 36em; padding: 5%; padding-top: 0;">
                                    <v-card-text v-if="verificated < 2" style="color: steelblue; padding-bottom: 0;">
                                        If the customer's name matches. Ask just one for level 1
                                    </v-card-text>
                                    <v-card-text v-else-if="verificated == 2" style="color: green; padding-bottom: 0;">
                                        Customer is level 1. Ask 1 question more for level 2 
                                    </v-card-text>
                                    <v-card-text v-else-if="verificated == 3" style="color: green; padding-bottom: 0;">
                                        Customer is level 2
                                    </v-card-text>
                                
                                    <div style="padding: 1em;" >
                                        <v-checkbox style="height: 1.5em;" label="Customer Service Pasword" @change="check_verification" v-model="CSP" />
                                        <span v-if="!CSP" style="font-size: 12px; margin-left: 6.8%; width: 100%; color: tomato;">
                                            Don't ask it if are the last 4 of social. Delete it if customer doesn't remember it
                                        </span>
                                        
                                        <v-checkbox style="margin-bottom: 0;" label="Drivers License Number"  @change="check_verification" v-model="SSN_DLN"/>
                                        

                                        <v-checkbox style="height: 1.5em;" label="Name of Joint Owners" v-model="JO" @change="check_verification"/>
                                        <span v-if="!JO" style="font-size: 12px; margin-left: 6.8%; width: 100%; color: steelblue; margin-bottom: 1.5em;">
                                            Ask only if customer has Joint Owners <span style="color: tomato; text-decoration: underline;">NOT</span> "Beneficiary"
                                        </span>

                                        <v-checkbox label="Amount of the Deposit" v-model="LD" @change="check_verification"/>

                                        <v-checkbox style="height: 1.5em;" label="Amount of the last ACH" v-model="ACH" @change="check_verification"/>
                                        <span style="font-size: 12px; margin-left: 6.8%; width: 100%; color: steelblue; margin-bottom: 1.5em;">
                                            Automatic credits and debits in the account
                                        </span>
                                        <v-checkbox label="Amount of the Check Cleared" v-model="CC" @change="check_verification"/>
                                        
                                        
                                    </div>
                                </v-card>
                            </div>

                            <div v-if="method == 'Debit Card Number'">  <!-- Debit Card Number -->
                                <v-card style="height: 36em; padding: 5%; padding-top: 0;">
                                    <v-card-text v-if="!SSN_DLN" style="color: steelblue; padding-bottom: 0;">
                                        Ask SSN or DL# + Two questions for level 1. 1 Question more for Level 2
                                    </v-card-text>
                                    <v-card-text v-if="verificated == 1" style="color: steelblue; padding-bottom: 0;">
                                        Two questions more level 1. 1 Question more for Level 2
                                    </v-card-text>
                                    <v-card-text v-if="verificated == 2" style="color: steelblue; padding-bottom: 0;">
                                        One question more level 1. 1 Question more for Level 2
                                    </v-card-text>
                                    <v-card-text v-else-if="verificated == 3" style="color: green; padding-bottom: 0;">
                                        Customer is level 1. Ask 1 question more for level 2 
                                    </v-card-text>
                                    <v-card-text v-else-if="verificated == 4" style="color: green; padding-bottom: 0;">
                                        Customer is level 2
                                    </v-card-text>
                                
                                    <div style="padding: 1em;" >
                                        <v-checkbox style="height: 1.5em;" label="Customer Service Pasword" 
                                        @change="check_verification" v-model="CSP" :disabled="!SSN_DLN" />
                                        <span v-if="!CSP" style="font-size: 12px; margin-left: 6.8%; width: 100%; color: tomato;">
                                            Don't ask it if are the last 4 of social. Delete it if customer doesn't remember it
                                        </span>
                                        
                                       <v-radio-group v-model="SSN_DLN" style="margin-top: 2em;" @change="check_verification">
                                            <v-radio style="margin-bottom: 10%;" label="Social Security Number" value="1" />
                                            <v-radio style="margin-bottom: 0;" label="Drivers License Number" value="2" />
                                            <!--Restar 1 al final-->
                                        </v-radio-group>
                                        

                                        <v-checkbox style="height: 1.5em;" label="Name of Joint Owners" v-model="JO" 
                                        @change="check_verification" :disabled="!SSN_DLN"/>
                                        <span v-if="!JO" style="font-size: 12px; margin-left: 6.8%; width: 100%; color: steelblue; margin-bottom: 1.5em;">
                                            Ask only if customer has Joint Owners <span style="color: tomato; text-decoration: underline;">NOT</span> "Beneficiary"
                                        </span>

                                        <v-checkbox label="Amount of the Deposit" v-model="LD" @change="check_verification" :disabled="!SSN_DLN"/>

                                        <v-checkbox style="height: 1.5em;" label="Amount of the last ACH" v-model="ACH" 
                                        @change="check_verification" :disabled="!SSN_DLN"/>
                                        <span style="font-size: 12px; margin-left: 6.8%; width: 100%; color: steelblue; margin-bottom: 1.5em;">
                                            Automatic credits and debits in the account
                                        </span>
                                        <v-checkbox label="Amount of the Check Cleared" v-model="CC" 
                                        @change="check_verification" :disabled="!SSN_DLN"/>
                                        
                                        
                                    </div>
                                </v-card>
                            </div>
                        </div>
                     
                           
                </v-expansion-panel-content>
            </v-expansion-panel>
                <h3 class="feature_item" >Self Service Options</h3>
                <h3 class="feature_item" >Further Assistance *</h3>
                <h3 class="feature_item" >Offer the Survey</h3>
                <h3 class="feature_item" >Closing with the name of the Branch *</h3>
            <v-expansion-panel>
                <v-expansion-panel-content style="box-shadow: 0 1px 0 0 rgb(209, 209, 209);" >
                    <div slot="header" class="transfer">Transfer the Call</div>
                    <v-card style="height: 24em;">
                        <Transfer />
                    </v-card>   
                    
                    
                </v-expansion-panel-content>
            </v-expansion-panel>
        </div>
        <div class="boolean_options">
            <v-switch id="switch_item" class="boolean_item" v-model="_1"/>
            <v-switch id="switch_item" class="boolean_item" v-model="_2"/>
            <v-switch id="switch_item" class="boolean_item" v-model="_3"/>
            <v-switch id="switch_item" class="boolean_item" v-model="verificated"/>
            <v-switch id="switch_item" class="boolean_item" v-model="_4"/>
            <v-switch id="switch_item" class="boolean_item" v-model="_5"/>
            <v-switch id="switch_item" class="boolean_item" v-model="_6"/>
            <v-switch id="switch_item" class="boolean_item" v-model="_7"/>
            <v-switch id="switch_item" class="boolean_item" v-model="sub_transfered"/>
            
            
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
    name: 'No_Customer_Info',
    components: {
        Transfer
    },
    data: () => ({
        disable_button: false,
        
        verificated: 0,
        CSP: 0,
        SSN_DLN: 0,
        JO: 0,
        LD: 0,
        ACH: 0,
        CC: 0,
        
        _1: 0, _2: 0, _3: 0, _4: 0, _5: 0, _6: 0, _7: 0,

        sub_transfered: 0,
        transfered: 0,
        value: 120,
        minute: 2,
        seconds: '00',
        pull_on_method: [
            {name: "Account Number", abbr: '', id: 1},
            {name: "Social Security Number", abbr: '', id: 2},
            {name: "Debit Card Number", abbr: '', id: 3}
        ],
        method: ''
    }),
    methods: {
        customFilter (item, queryText, itemText) {
            const textOne = item.name.toLowerCase()
            const textTwo = item.abbr.toLowerCase()
            const searchText = queryText.toLowerCase()

            return textOne.indexOf(searchText) > -1 ||
            textTwo.indexOf(searchText) > -1
        },
        
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

        checking() {
            console.log("CSP: "+this.CSP+" SSN or DLN: "+this.SSN_DLN+" JO: "+this.JO+" LD: "+this.LD+" ACH: "+this.ACH+" CC: "+this.CC);
        },
        check_verification() {
            let c_csp = 0, c_jo = 0, c_ld = 0, c_ach = 0, c_cc = 0, c_ssn_dln;

            this.CSP ? c_csp = 1 : c_csp = 0 
            this.JO ? c_jo = 1 : c_jo = 0 
            this.LD ? c_ld = 1 : c_ld = 0
            this.ACH ? c_ach = 1 : c_ach = 0
            this.CC ? c_cc = 1 : c_cc = 0
            this.SSN_DLN == 1 || this.SSN_DLN == 2 ? c_ssn_dln = 1 : c_ssn_dln = 0;
            
            this.verificated = c_csp + c_jo + c_ld + c_ach + c_cc + c_ssn_dln;
            console.log(this.verificated);
        },
        refresh_values () {
            this._1 = 0; 
            this._2 = 0; 
            this._3 = 0; 
            this._4 = 0; 
            this._5 = 0; 
            this._6 = 0; 
            this._7 = 0;
            this.verificated = 0;
            this.sub_transfered = 0;
        }
    },
    mounted() {
        this.minute = 2;
        this.seconds = 60;
        this.seconds == 60 ? this.seconds = '00' : this.seconds = 59
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
        background: white;
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
    .countdown {
        background: white;
        color: #009688;
        width: 3em;
        height: 3em;
        border-radius: 50%;
        position: absolute;
        right: 10.3%;
        margin-top: .4%;
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 2;
    }
</style>
