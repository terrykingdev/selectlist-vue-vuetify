<template>
  <v-app>
    <v-main>
      <v-container fluid>
        <v-row>
          <v-col cols="4">
            <SelectList :list="availableOutputFields" :selectedList="availableOutputFieldsSelected" @dblclick="addThis"/>
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
            <SelectList :list="outputFields" :selectedList="outputFieldsSelected" @dblclick="removeThis"/>
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
    // Double click item is a quick add
    addThis(item){
      // Check if already added
      if (this.outputFields.findIndex(x => x.text == item.text)<0){
        this.outputFields.push(item)
      }
    },
    removeThis(item,index){
      this.outputFields.splice(index,1)
      // Clear all selected
      this.outputFieldsSelected = []
    },
    addField(){
      // Add all selected fields
      for(let i in this.availableOutputFieldsSelected){
        let item=this.availableOutputFields[this.availableOutputFieldsSelected[i]]
        // Check if it's already added
        if (this.outputFields.findIndex(x => x.text == item.text)<0){
          this.outputFields.push(item)
        }
      }
    },
    removeField(){
      // Remove all selected fields
      for(let i=this.outputFieldsSelected.length-1;i>=0;i--){
        this.outputFields.splice(this.outputFieldsSelected[i],1)
        this.outputFieldsSelected.pop()
      }
    },
    moveUp(){
      // Move all selected fields up one
      if (this.outputFieldsSelected.length>0 && this.outputFieldsSelected[0]>0){
        for(let i=this.outputFieldsSelected.length-1;i>=0;i--){
          let index=this.outputFieldsSelected[i]
          this.outputFields[index] = this.outputFields.splice(index-1, 1, this.outputFields[index])[0]; // exchange shortcut
        }
        // Reduce all selected indexes by one
        this.outputFieldsSelected = this.outputFieldsSelected.map(x => x-1)
      }
    },
    moveDown(){
      // Move all selected fields down one
      if (this.outputFieldsSelected.length>0 && this.outputFieldsSelected[this.outputFieldsSelected.length-1]<this.outputFields.length-1){
        for(let i=this.outputFieldsSelected.length-1;i>=0;i--){
          let index=this.outputFieldsSelected[i]
          this.outputFields[index] = this.outputFields.splice(index+1, 1, this.outputFields[index])[0]; // exchange shortcut
        }
        // Increase all selected indexes by one
        this.outputFieldsSelected = this.outputFieldsSelected.map(x => x+1)
      }
    },
  }
};
</script>

