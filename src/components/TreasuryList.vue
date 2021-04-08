<template>
    <div>
        <v-data-table
            class="mt-10 elevation-20"
            :items="treasuries"
            :items-per-page="9999"
        >
            <!-- TEMPLATE -->
            <template>
                <tr>
                    <td>
                        {item}
                    </td>
                    <td>
                        {index}
                    </td>
                </tr>
            </template>        
        </v-data-table>
        
    </div>
</template>

<script>
    import axios from 'axios';
    
    export default {
        name: 'TreasuryList',
        mounted: function() {
            axios.get("https://bitcointreasuries.org/").then(response => {
                debugger;
                console.log(response);
            }).catch(function (error) {
                alert("Error: " + error);
            })
            ;
        },
        data () {
          return {
              treasuries: [],
              ajaxCurrentlyBusy: true,
              tableHeader: [
                  { text: "Sel?", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "Note", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "Company", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "Symbol", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "Market Cap", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "% BTC", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "Purchase / Filing", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "Cost Basis USD", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "Today's Value", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "NgU", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "₿ Amount", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "/21M", value: "arrayIndex", width: "175px", class: "VerticalText"}          
                ]
            }
        },
    }
</script>