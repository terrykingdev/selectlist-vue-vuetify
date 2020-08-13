<template>
  <v-app>
    <v-main>
      <v-container fluid>

        <v-row>
          <v-col cols="4">
            <SelectList :list="availableOutputFields" :selectedList="availableOutputFieldsSelected" />
          </v-col>
          <v-col cols="2" class="d-flex flex-column justify-space-around px-3">
            <v-btn @click="addField()" class="mx-2" fab dark small color="primary">
              <v-icon dark>mdi-arrow-right-circle</v-icon>
            </v-btn>
            <v-btn @click="removeField()" class="mx-2" fab dark small color="primary">
              <v-icon dark>mdi-arrow-left-circle</v-icon>
            </v-btn>
          </v-col>
          <v-col cols="4">
            <SelectList :list="outputFields" :selectedList="outputFieldsSelected" />
          </v-col>
          <v-col cols="2" class="d-flex flex-column justify-space-around px-3">
            <v-btn @click="moveUp()" class="mx-2" fab dark small color="primary">
              <v-icon dark>mdi-arrow-up-circle</v-icon>
            </v-btn>
            <v-btn @click="moveDown()" class="mx-2" fab dark small color="primary">
              <v-icon dark>mdi-arrow-down-circle</v-icon>
            </v-btn>
          </v-col>
        </v-row>

      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import SelectList from './components/SelectList'

export default {
  name: 'App',
  data: function(){
    return {
      outputFields: [
        { text: 'Antenna Port', value: 'antennaport'},
      ],
      outputFieldsSelected: [],
      availableOutputFieldsSelected: [],
      availableOutputFields: [
        { text: 'Antenna Port', value: 'antennaport'},
        { text: 'Timestamp', value: 'timestamp'},
        { text: 'Peak RSSI', value: 'rssi'},
        { text: 'TID', value: 'tid'},
        { text: 'User Memory', value: 'usermem'},
        { text: 'EPC', value: 'epc'}
      ],
     }
  },
  components: {
    SelectList
  },
  methods:{
    addField(){
      for(let i in this.availableOutputFieldsSelected){
        let found=false
        for(let j in this.outputFields){
          if (this.outputFields[j].text==this.availableOutputFields[this.availableOutputFieldsSelected[i]].text){
            found=true
          }
        }
        if (!found){
          this.outputFields.push(this.availableOutputFields[this.availableOutputFieldsSelected[i]])
        }
      }
    },
    removeField(){
      for(let i=this.outputFieldsSelected.length-1;i>=0;i--){
        this.outputFields.splice(this.outputFieldsSelected[i],1)
        this.outputFieldsSelected.pop()
      }
    },
    moveUp(){
      if (this.outputFieldsSelected.length>0 && this.outputFieldsSelected[0]>0){
        for(let i=this.outputFieldsSelected.length-1;i>=0;i--){
          let index=this.outputFieldsSelected[i]
          let tmp=this.outputFields[index]
          this.outputFields.splice(index,1)
          this.outputFields.splice(index-1,0,tmp)
        }
        this.outputFieldsSelected = this.outputFieldsSelected.map(x => x-1)
      }
    },
    moveDown(){
      if (this.outputFieldsSelected.length>0 && this.outputFieldsSelected[this.outputFieldsSelected.length-1]<this.outputFields.length-1){
        for(let i=this.outputFieldsSelected.length-1;i>=0;i--){
          let index=this.outputFieldsSelected[i]
          let tmp=this.outputFields[index]
          this.outputFields.splice(index,1)
          this.outputFields.splice(index+1,0,tmp)
        }
        this.outputFieldsSelected = this.outputFieldsSelected.map(x => x+1)
      }
    },
  }
};
</script>

