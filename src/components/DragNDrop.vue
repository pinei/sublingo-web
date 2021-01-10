<template>
  <div id="drop_zone" @drop="dropHandler" @dragenter.prevent @dragover.prevent :class="highlightClass">
    <p>Drag one or more files to this Drop Zone ...</p>
  </div>
</template>

<script>
export default {
  name: 'DragNDrop',
  data() {
    return {
      highlightClass: ''
    };
  },
  props: {
    msg: String
  },
  methods: {
    dropHandler: function(ev) {
      // Prevent default behavior (Prevent file from being opened)
      ev.preventDefault();
      ev.stopPropagation();

      console.log('File(s) dropped');

      if (ev.dataTransfer.items) {
        // Use DataTransferItemList interface to access the file(s)
        for (var i = 0; i < ev.dataTransfer.items.length; i++) {
          // If dropped items aren't files, reject them
          if (ev.dataTransfer.items[i].kind === 'file') {
            console.log('... '+ ev.dataTransfer.items[i])
            // var file = ev.dataTransfer.items[i].getAsFile();
            // console.log('... file[' + i + '].name = ' + file.name);
          }
        }
      } else {
        // Use DataTransfer interface to access the file(s)
        for (i = 0; i < ev.dataTransfer.files.length; i++) {
          console.log('... file[' + i + '] = ' + ev.dataTransfer.files[i]);
        }
      }
    },

    dragHandler: function(ev) {
      console.log(ev)
      // Prevent default behavior (Prevent file from being opened)
      ev.preventDefault();

      console.log('dragEnter')
      this.highlightClass = 'highlightDropArea'

      if (ev.dataTransfer.items) {
        // Use DataTransferItemList interface to access the file(s)
        for (var i = 0; i < ev.dataTransfer.items.length; i++) {
          // If dropped items aren't files, reject them
          if (ev.dataTransfer.items[i].kind === 'file') {
            // var file = ev.dataTransfer.items[i].getAsFile();
            console.log('... item[' + i + '] = ' + JSON.stringify(ev.dataTransfer.items[i]));
          }
        }
      } else {
        // Use DataTransfer interface to access the file(s)
        for (i = 0; i < ev.dataTransfer.files.length; i++) {
          console.log('... file[' + i + '] = ' + JSON.stringify(ev.dataTransfer.files[i]));
        }
      }
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #drop_zone {
    width:  400px;
    height: 400px;
  }
  .solidDropArea {
    border: 5px solid blue;
  } 

  .highlightDropArea {
    border: 5px green dashed;
  }
</style>
