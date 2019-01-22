<template>
    <div class="main_transfer_container">
      <v-autocomplete
        :items="departments"
        :filter="customFilter"
        color="blue"
        item-text="name"
        label="Department Name"
        autofocus
        light
        v-model="department"
      ></v-autocomplete>

      <div v-if="department">
        <div v-if="department == 'Loans'">
            <v-sheet class="Loans" color="blue lighten-3" height="100%">
                <h3 style="padding-bottom: 2%; color: rgb(8, 83, 145);">Loans (#4003) </h3>
                <p style="color: rgb(8, 83, 145);">Full Number: 1 800 239-1996</p>
                <p style="font-weight: bolder; color: rgb(8, 83, 145);">Give this number to the customer</p>
                <div class="Important_Info">
                    <span>If the customer is already verified do a <span style="color: tomato;">Warm Transferm.</span> Else, do a 
                        <span style="color: blue;">Cold Transfer</span> </span>
                </div>
            </v-sheet>
        </div>

        <div v-if="department == 'Bank Cards'">
            <v-sheet class="Bank_Cards" color="blue lighten-3" height="100%">
                <h3 style="padding-bottom: 2%; color: rgb(8, 83, 145);">Bank Cards (#4004) </h3>
                <p style="color: rgb(8, 83, 145);">Full Number: 1-800-239-5175</p>
                <p style="font-weight: bolder; color: rgb(8, 83, 145);">Give this number to the customer</p>
                <div class="Important_Info">
                    <span>If the customer is already verified do a <span style="color: tomato;">Warm Transferm.</span> Else, do a 
                        <span style="color: blue;">Cold Transfer. </span> 
                        Remember that the Bank Cards department has a verification process different from ours.
                    </span>
                </div>
            </v-sheet>
        </div>

        <div v-if="department == 'Disputes'">
            <v-sheet class="Bank_Cards" color="blue lighten-3" height="100%">
                <h3 style="padding-bottom: 2%; color: rgb(8, 83, 145);">Disputes (#4011) </h3>
                <p style="color: rgb(8, 83, 145);">Full Number: 1-800-XXX-XXXX</p>
                <p style="font-weight: bolder; color: rgb(220, 88, 10);">Do not give this number to the customers. Verify the customer on lvl 2 (1 Question)</p>
                <div class="Important_Info">
                    <span>
                    Always make a Warm Transfer, you need to know about the dispute reason. 
                    If the dispute proccess was already begun, <span style="color: #FF791E"> Verify the customer on lvl 2 and ask for the dispute number.</span> 
                    Be careful with the time in hold. <span style="color: green; font-weight: bold">It is recommended to use the Hold Tracker.</span>
                    </span>
                </div>
            </v-sheet>
        </div>

      </div>
    </div>
</template>

<script>
export default {
    name: 'Transfer',
    data: () => ({
        departments: [
                { name: 'Loans', abbr: "L", id: 1},
                { name: 'Bank Cards', abbr: "BC", id: 2},
                { name: 'Disputes', abbr: "D", id: 3}
            ],
        department: ""
    }),
    methods: {
      customFilter (item, queryText, itemText) {
        const textOne = item.name.toLowerCase()
        const textTwo = item.abbr.toLowerCase()
        const searchText = queryText.toLowerCase()

        return textOne.indexOf(searchText) > -1 ||
          textTwo.indexOf(searchText) > -1
      },
    }
}
</script>

<style>
    .main_transfer_container {
        padding: 1em;
        background: white;
        height: 10em;

    }
    .Important_Info {
        width: 100%;
        background: rgba(0, 204, 0, .3);
        text-align: justify;
        padding: 1%;
        color: white;
    }
    .Loans {
        padding: 1em;
        color: white;
    } 
    .Bank_Cards {
        padding: 1em;
        color: white;
        padding-bottom: 1em;
    }
    

</style>
