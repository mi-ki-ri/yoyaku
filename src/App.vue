<template>
  <div id="app">
    <div class="container h-screen flex justify-start items-stretch flex-col">
      <header class="h-10">
        <h1 class="text-center">YOYAKU</h1>
      </header>
      <main class="h-screen flex justify-center items-stretch flex-row">
        <section class="flex-grow">
          <textarea
            v-model="textForItems"
            @keydown.tab="onTab"
            class="h-screen w-full"
          >
          </textarea>
        </section>
        <section class="flex-grow-0">
          <ul>
            <li v-for="(task, i) in itemsFromText" :key="i">
              {{ task }}
            </li>
          </ul>
        </section>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      textForItems: "",
    };
  },
  computed: {
    itemsFromText() {
      const lines = this.textForItems.split("\n");

      const objs = []

      lines.forEach((line) => {
        const obj = {}
        const matches = line.match(/^(\t*)([^\t]*)/i);
        if (matches.length == 3){
          const level = matches[1].length
          const text = matches[2]
          obj.level = level
          obj.text = text
          
        }
        console.log(obj)
        objs.push(obj)
      });

      return objs;
    },
  },
  methods: {
    onTab(e) {
      // TAB入力
      e.preventDefault(); 

      var elem = e.target;
      var val = elem.value;
      var pos = elem.selectionStart;
      elem.value = val.substr(0, pos) + "\t" + val.substr(pos, val.length);
      elem.setSelectionRange(pos + 1, pos + 1);
    },
  },
};
</script>

<style>
#app {
  color: #2c3e50;
}
</style>
