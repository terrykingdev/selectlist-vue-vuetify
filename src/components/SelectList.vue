<template>
   <v-list dense>
      <v-list-item-group >
        <v-list-item
          v-for="(item, i) in list"
          @click="clickList($event,item,i)"
          @dblclick="$emit('dblclick',item,i)"
          :key="i"
          :class="isSelected(i)?'selectlisthighlighted':''"          
          >
          <v-list-item-content>
            <v-list-item-title v-text="item.text"></v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>    
</template>

<script>
export default {
  name: 'SelectList',
  data: function () {
    return {
      selectedList_last: null
    }
  },
  props: [
    'list',
    'selectedList'
  ],
  methods: {
    isSelected(index) {
      let found = false
      for (let i in this.selectedList) {
        if (this.selectedList[i] == index) {
          found = true
        }
      }
      return found
    },
    clickList(event, item, index) {
      let shift = event.shiftKey
      let ctrl = event.ctrlKey
      if (!shift && !ctrl) {
        while (this.selectedList.length > 0) {
          this.selectedList.pop()
        }
        this.selectedList.push(index)
        this.selectedList.sort()
        this.selectedList_last = index
      } else if (!shift && ctrl) {
        let found = false
        for (let i in this.selectedList) {
          if (this.selectedList[i] == index) {
            found = true
          }
        }
        if (!found) {
          this.selectedList.push(index)
        }
        this.selectedList.sort()
        this.selectedList_last = index
      } else if (shift && !ctrl) {
        while (this.selectedList.length > 0) {
          this.selectedList.pop()
        }
        if (this.selectedList_last < index) {
          for (let i = this.selectedList_last; i <= index; i++) {
            this.selectedList.push(i)
          }
        } else {
          for (let i = index; i <= this.selectedList_last; i++) {
            this.selectedList.push(i)
          }
        }
        this.selectedList.sort()
      }
    },
  }
}
</script>

<style scoped>
.selectlisthighlighted{
  background-color:cadetblue;
}
</style>