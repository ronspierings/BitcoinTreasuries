<template>
    <div>
        <div id="dataTmp">
        </div>
        <v-card>
            <v-card-title>
              Zoek
                <v-spacer></v-spacer>
              <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                label="Zoeken"
                single-line
                hide-details
              ></v-text-field>
            </v-card-title>
            <v-data-table
                class="mt-10 elevation-20"
                :items="treasuries"
                :headers="tableHeader"
                :items-per-page="9999"
            >
                <!-- TEMPLATE -->
                <template 
                    v-slot:item="{ item }"
                    show-select
                >
                    <tr>
                        <td>
                            {{item.rank}}
                        </td>
                        <td>
                            {{item.category}}
                        </td>                    
                        <td>
                            {{item.company}}
                        </td>
                        <td>
                            {{item.country}}
                        </td>
                        <td>
                            {{item.symbol}}
                        </td>
                        <td>

                        </td>
                        <td>

                        </td>
                        <td>

                        </td>
                        <td>

                        </td>
                        <td>

                        </td>
                        <td>

                        </td>
                        <td>

                        </td>
                        <td>

                        </td>
                    </tr>
                </template>
            </v-data-table>  
        </v-card>
    </div>
</template>

<script>
    import axios from 'axios';
    //import sheetrock from 'sheetrock';
    
    export default {
        name: 'TreasuryList',
        mounted: function() {
            
            axios.get("http://www.r-spierings.nl/treasuries/index.php")
            .then(response => {
                
                this.treasuries = [];
                
                // Every treasury record is inside a TR. Retrieve them as a array
                var treasuries = $(".waffle tbody tr", response.data).toArray();
                
                // The first element are the columnheaders. Remove them
                treasuries.shift();
                    
                // Loop through every treasurie record (and collect the columns as jquery objects)
                var rank = 1;
                for(let $row of treasuries)
                {
                    var treasurieRow = {};
                    
                    // From a record, the row data is inside a TD. Retrieve them.
                    var columns = $("td", $row).toArray();
                    
                    // Rank
                    treasurieRow.rank = rank;
                    // Cat
                    treasurieRow.category = "Private";
                    // Company
                    treasurieRow.company = columns[1].innerText;
                    // Country
                    treasurieRow.country = columns[2].innerText;
                    // Symbol
                    treasurieRow.symbol = columns[3].innerText;
                    // Marketcap
                    // % BTC
                    // Purchase / filings
                    // Cost Basis USD
                    // Today Value
                    // NgU
                    // B amount
                    // / 21M
                    
                    rank++;
                    
                    // Add row to the collection
                    this.treasuries.push(treasurieRow);
                }

                
            });
        },
        data () {
          return {
              treasuries: [],
              ajaxCurrentlyBusy: true,
              tableHeader: [
                  { text: "Rank", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "Category", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  //{ text: "Note", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "Company", value: "arrayIndex", width: "175px", class: "VerticalText"},
                  { text: "Country", value: "arrayIndex", width: "175px", class: "VerticalText"},
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