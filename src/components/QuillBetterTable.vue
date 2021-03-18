<template>
  <div>
    <div>
      <h3>Insert table and click on the table to wake up the table column tools. <br>Right-click on table to show operations menu.<br>
      </h3>
      <div class="btn-group">
        <button v-on:click="insertTable">Insert table</button>
        <button v-on:click="getTable">Get table</button>
        <button v-on:click="getContents">Get contents</button>
      </div>
    </div>
    <div id="editor"></div>
    <h3>Delta formats</h3>
    <p id="delta-view"></p>
  </div>
</template>

<script>
import Quill from "quill";
import "quill/dist/quill.core.css";
import "quill/dist/quill.snow.css";
import "quill/dist/quill.bubble.css";
import QuillBetterTable from "quill-better-table";

Quill.register({
  "modules/better-table": QuillBetterTable
}, true);

export default {
  mounted: function() {
    this.editor = new Quill("#editor", {
      theme: 'snow',
      modules: {
        table: false,
        'better-table': {
          operationMenu: {
            items: {
              unmergeCells: {
                text: 'Another unmerge cells name'
              }
            },
            color: {
              colors: ['green', 'red', 'yellow', 'blue', 'white'],
              text: 'Background Colors:'
            }
          }
        },
      }
    });
  },
  methods: {
    insertTable: function () {
      this.editor.getModule('better-table').insertTable(3, 3);
    },
    getTable: function () {
      console.log(this.editor.getModule('better-table').getTable());
    },
    getContents: function () {
      document.body.querySelector('#delta-view')
        .innerHTML = JSON.stringify(
          this.editor.getContents()
        )
    },
  },
};
</script>
