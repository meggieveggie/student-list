<template>
  <v-container fluid grid-list-md>
    <v-layout row wrap>
      <v-flex xs3>
        <v-avatar size="150px" class="avatar">
          <img :src="student.pic" alt="avatar" />
        </v-avatar>
      </v-flex>
      <v-layout>
        <v-flex xs8>
          <v-card-text>
            <h1>{{ student.firstName | capitalize }} {{ student.lastName | capitalize }}</h1>
            <p class="student-info">
              Email: {{student.email}}
              <br />
              Company: {{student.company}}
              <br />
              Skill: {{student.skill}}
              <br />
              Average: {{studentAverage(student.grades)}}%
              <br />
              <br />
              <span v-if="showGrades">
               <span v-for="(grade, index) in student.grades" v-bind:key="index">
                Test {{index+1}} &nbsp; &nbsp; &nbsp; {{grade}}%
                <br />
               </span> 
                </span>
            </p>
            <v-flex v-if="showGrades" class="student-info" xs4>
            <v-chip label v-for="(tag, tagIndex) in student.tags" v-bind:key="tagIndex">
                {{tag}}
            </v-chip>
             <v-text-field 
            @keyup.enter="addTag" 
            placeholder="Add a tag" 
            v-model="tag">
            </v-text-field>
            </v-flex>
          </v-card-text>
        </v-flex>
      </v-layout>
      <v-flex sx1 class="text-lg-right">
            <v-icon v-if="!showGrades" x-large @click="showGrades=!showGrades"> add </v-icon>
            <v-icon v-if="showGrades" x-large @click="showGrades=!showGrades"> remove </v-icon>
        </v-flex>
    </v-layout>
     <v-divider></v-divider>
  </v-container>
</template>

<script>
export default {
  props: {
    student: Object,
    index: Number
  },

  data: () => ({
       showGrades: false,
       tag: ''
  }),

  methods: {
    studentAverage: function(grades) {
      var sum = 0;
      for (var i = 0; i < grades.length; i++) {
        sum += parseInt(grades[i])
      }
      return sum / grades.length
    },
    addTag: function() {
        this.$emit('tag-added', {
            index: this.index,
            tag: this.tag
        })
        this.tag = ''
    }
  },

  filters: {
    capitalize: function(value) {
      if (!value) return "";
      value = value.toString();
      return value.toUpperCase();
    }
  }
}
</script>

<style>
.student-info {
  padding-left: 20px;
  color: gray;
}
</style>