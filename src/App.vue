<template>
  <div id="app">
    <section id="example-1">
      <h1>Example 1 (Single, Filterable)</h1>
      <hr>
      <div class="examples">
        <b>1) Array input</b>:
        <pre>
          {{itemsExampleFirst}}
        </pre>
        <b>2) (labelProp)Property for display in label: 'title'; (keyProp) 'id'</b>
        <br><br>
        <b>3) Output values:</b>
        <br>
        <pre>{{resultExampleFirst}}</pre>
        <yyn-custom-select
            v-model="resultExampleFirst"
            :placeHolder="'Example 1'"
            :items="itemsExampleFirst"
            :keyProp="'id'"
            :labelProp="'title'"
            :isFilterable="true"
        />
      </div>
    </section>
    <section id="example-2">
      <h1>Example 2 (Multiple)</h1>
      <hr>
      <div class="examples">
        <b>1) Array input</b>:
        <pre>
          {{itemsExampleSecond}}
        </pre>
        <b>2) (labelProp)Property for display in label: 'name'; (keyProp) 'id'</b>
        <br><br>
        <b>3) Output values:</b>
        <br>
        <pre>{{resultExampleSecond}}</pre>
        <yyn-custom-select
            v-model="resultExampleSecond"
            :placeHolder="'Example 1'"
            :items="itemsExampleSecond"
            :keyProp="'id'"
            :labelProp="'name'"
            :isMultiple="true"
        />
      </div>
    </section>
    <section id="example-3">
      <h1>Example 3 (Multiple, Filterable)</h1>
      <hr>
      <div class="examples">
        <b>1) Array input</b>:
        <pre>
          {{itemsExampleThird}}
        </pre>
        <b>2) (labelProp)Property for display in label: -; (keyProp) -</b>
        <br><br>
        <b>3) Output values:</b>
        <br>
        <pre>{{resultExampleThird}}</pre>
        <yyn-custom-select
            v-model="resultExampleThird"
            :placeHolder="'CustomSelect'"
            :items="itemsExampleThird"
            :isMultiple="true"
            :isFilterable="true"
        />
      </div>
    </section>
  </div>
</template>

<script>

import YynCustomSelect from './components/yyn-custom-select'
export default {
  name: 'App',
  components: { YynCustomSelect },
  data: () => ({
    // example 1
    resultExampleFirst: null,
    itemsExampleFirst: [
      {
        "id": 1,
        "title": "delectus aut autem",
        "completed": false
      },
      {
        "id": 2,
        "title": "quis ut nam facilis et officia qui",
        "completed": false
      },
      {
        "id": 3,
        "title": "fugiat veniam minus",
        "completed": false
      },
      {
        "id": 4,
        "title": "et porro tempora",
        "completed": true
      }
    ],
    // example 2
    resultExampleSecond: null,
    itemsExampleSecond: [
      {
        "id": 1,
        "name": "delectus",
        "completed": false
      },
      {
        "id": 2,
        "name": "quis ut nam facilis et officia qui",
        "completed": false
      },
      {
        "id": 3,
        "name": "fugiat veniam minus",
        "completed": false
      },
      {
        "id": 4,
        "name": "et porro tempora",
        "completed": true
      }
    ],
    // example 3 third
    resultExampleThird: null,
    itemsExampleThird: ['js', 'vue', 'angular', 'docker', 'nestjs', 'sql']
  })
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.examples {
  text-align: left;
}
pre {
  background-color: #ededed;
}
</style>
