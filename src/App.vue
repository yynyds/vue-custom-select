<template>
  <div id="app">
<!--    <section id="example-1">
      <h1>Example 1 (Single, Filterable)</h1>
      <hr>
      <div class="examples">
        <b>1) Array input</b>:
        <pre>
          {{itemsExample1}}
        </pre>
        <b>2) (labelProp)Property for display in label: 'title'; (valueProp)Property for value in output: 'id'; (keyProp) 'id'</b>
        <br><br>
        <b>3) Output values:</b>
        <br>
        <pre>{{myValueInCS_1}}</pre>
        <CustomSelect
            v-model="myValueInCS_1"
            :items="itemsExample1"
            :labelProp="'title'"
            :valueProp="'id'"
            :keyProp="'id'"
            :isFilterable="true"
            :isMultiple="false"
        />
      </div>
    </section>
    <section id="example-2">
      <h1>Example 2 (Multiple)</h1>
      <hr>
      <div class="examples">
        <b>1) Array input</b>:
        <pre>
          {{itemsExample2}}
        </pre>
        <b>2) (labelProp)Property for display in label: 'name'; (valueProp)Property for value in output: 'name'; (keyProp) 'id'</b>
        <br><br>
        <b>3) Output values:</b>
        <br>
        <pre>{{myValueInCS_2}}</pre>
        <CustomSelect
            v-model="myValueInCS_2"
            :items="itemsExample2"
            :labelProp="'name'"
            :valueProp="'name'"
            :keyProp="'id'"
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
          {{itemsExample3}}
        </pre>
        <b>2) (labelProp)Property for display in label: -; (valueProp)Property for value in output: -; (keyProp) -</b>
        <br><br>
        <b>3) Output values:</b>
        <br>
        <pre>{{myValueInCS_3}}</pre>
        <CustomSelect
            v-model="myValueInCS_3"
            :items="itemsExample3"
            :isFilterable="true"
            :isMultiple="true"
        />
      </div>
    </section>-->
    <yyn-custom-select
        v-model="myValue"
        :placeHolder="'CustomSelect'"
        :items="itemsExample"
        :keyProp="'id'"
        :labelProp="'title'"
        :valueProp="'title'"
        :isMultiple="false"
        :isFilterable="true"
    />
    {{myValue}}
  </div>
</template>

<script>

import YynCustomSelect from './components/yyn-custom-select'
export default {
  name: 'App',
  components: { YynCustomSelect },
  data: () => ({
    // example 1
    myValue: null,
    itemsExample: [
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
</style>
