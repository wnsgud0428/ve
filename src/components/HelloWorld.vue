<template>
  <v-container>
    <v-card>
      <v-toolbar dense flat>
        <v-toolbar-title>문서편집기</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn icon>
          <v-icon>mdi-eye</v-icon>
        </v-btn>
      </v-toolbar>
      <v-card-text> <!--text 타이핑 할수있게 넣음-->
        <v-textarea v-model="text"></v-textarea>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn @click="read">read</v-btn>
        <v-btn @click="write">write</v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script>
const { dialog } = require('electron').remote
const fs = require('fs')
export default {
  data () {
    return {
      text: ''
    }
  },
  methods: {
    read () {
      const options = {
        filters: [
          {
            name: 'text and markdown',
            extensions: ['txt', 'md']
          }
        ]
      }
      const r = dialog.showOpenDialogSync(options)
      if (!r) return
      this.text = fs.readFileSync(r[0])
    },
    write () {
      const options = {
        filters: [
          {
            name: 'text and markdown',
            extensions: ['txt', 'md']
          }
        ]
      }
      const r = dialog.showSaveDialogSync(options)
      // console.log(r)
      if (!r) return
      fs.writeFileSync(r, this.text)
    }
  }
}

</script>
