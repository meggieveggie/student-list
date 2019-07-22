<template>
 <v-flex xs12>
    <v-container>
            <v-card class="students-container scroll-y">
              <v-text-field v-model="filter" class="name-input" placeholder="Search by name" color="gray" ></v-text-field>
              <v-text-field class="tag-input" v-model="tagFilter" placeholder="Search by tag" color="gray" ></v-text-field>
              <Student 
              v-for="(student, index) in filtedStudents"
              v-bind:key="student.id"
              :student="student"
              :index="index"
              @tag-added="tagAdded"
              />
            </v-card>
             </v-container>
  </v-flex>
</template>

<script>
import studentData from '../../students.json'
import Student from "./Student";

  export default {
    mounted: function() {
    this.getStudents();
  },

  components: {
    Student
  },

   data: () => ({
    students: [],
    filter: null,
    tagFilter: null
   }),

   methods: {
    getStudents: function() {
      this.students = studentData.students
    },
    tagAdded: function(value) {
      if (this.students[value.index].tags) {
        this.students[value.index].tags.push(value.tag)
      } else {
        this.students[value.index].tags = [value.tag]
      }
    },
     filterByName: function(studentList) {
      var currentScope = this
      if (this.filter) {
        return studentList.filter(function(el) {
          return (
            el.firstName.toUpperCase().includes(currentScope.filter.toUpperCase()) ||
            el.lastName.toUpperCase().includes(currentScope.filter.toUpperCase())
          )
        })
      }
      return studentList;
    },

    filterByTags: function(studentList) {
      var currentScope = this
      if (this.tagFilter) {
        return studentList.filter(function(el) {
          if (el.tags) {
            return el.tags.includes(currentScope.tagFilter)
          }
          return false
        })
      }
      return studentList
    }
   },

   computed: {
    filtedStudents() {
      var studentList = this.students
      studentList = this.filterByName(studentList)
      studentList = this.filterByTags(studentList)
      return studentList
    }
  }
  }

</script>

<style>
.students-container {
  max-height: 800px;
}

.name-input {
  padding: 15px 15px 0px 15px;
  font-family: 'Cairo', sans-serif;
  font-size: 20px;
}
.tag-input {
  padding: 0px 15px 0px 15px;
  font-family: 'Cairo', sans-serif;
  font-size: 20px;
}
</style>