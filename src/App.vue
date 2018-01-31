<template>
  <div class="container-fluid">
    <div class="row">
      <div id="app">
        <div class="jumbotron">
          <h1 class="display-4">School</h1>

          <p>
            All Students: <span class="badge badge-info">{{ totalStudents }}</span>
            Class #1: <span class="badge badge-success">{{ totalStudentsOne }}</span>
            Class #2: <span class="badge badge-warning">{{ totalStudentsTwo }}</span>
          </p>

          <hr class="my-4">

          <div class="row">
            <div class="col-sm-6 col-xs-12">
              <div class="form-group">
                <label for="newStudent">Name</label>
                <input type="text" class="form-control" v-model="newStudent">
              </div>

              <div class="form-group">
                <button @click="addNewStudent" class="btn btn-info">Add New Student</button>
              </div>
            </div>

            <div class="col-sm-6 col-xs-12">
              <label>Students to divide</label>

              <ul class="list-group">
                <li class="list-group-item" v-for="(student, index) in students">{{ student }} <br> <button class="btn btn-success" @click="addToClass(student, index, 1)">Add to #1</button> <button class="btn btn-warning" @click="addToClass(student, index, 2)">Add to #2</button></li>
              </ul>
            </div>
          </div>
        </div>

        <div class="col-sm-12">
          <div class="row">
            <app-class-one :student="classOneStudent" v-on:decrease="leaveSchool" v-on:return="returnedStudentOne" v-on:increase="increase"></app-class-one>
            <app-class-two :student="classTwoStudent" v-on:decrease="leaveSchool" v-on:return="returnedStudentTwo" v-on:increase="increase"></app-class-two>
          </div>

          <hr>

          <p class="text-center">&copy; 2018</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ClassOne from './components/ClassOne.vue';
import ClassTwo from './components/ClassTwo.vue';

export default {
  data () {
    return {
      newStudent: "",
      students: ["Peter", "Michael", "Kevin", "Hanna", "Lisa", "Paul", "Linda"],
      classOneStudent: "",
      classTwoStudent: "",
      totalStudents: 0,
      totalStudentsOne: 0,
      totalStudentsTwo: 0,
    }
  },
  components: {
    appClassOne: ClassOne,
    appClassTwo: ClassTwo
  },
  methods: {
  	addNewStudent: function(){
    	this.students.push(this.newStudent);
      this.totalStudents++;
      this.newStudent = '';
    },
    addToClass: function(student, index, className){
    	this.students.splice(index, 1);
      switch( className ){
      	case 1:
       		this.classOneStudent = student;
      		this.totalStudentsOne++;
          break;
        case 2:
          this.classTwoStudent = student;
      		this.totalStudentsTwo++;
          break;
      }
    },
    leaveSchool: function(className){
    	 switch( className ){
      	case 1:
       		this.totalStudentsOne--;
          break;
        case 2:
          this.totalStudentsTwo--;
          break;
      }
    	this.totalStudents--;
    },
    returnedStudentOne: function(student){
    	this.students.push(student);
      this.totalStudentsOne--;
    },
    returnedStudentTwo: function(student){
    	this.students.push(student);
      this.totalStudentsTwo--;
    },
    increase: function(className){
    	switch( className ){
      	case 1:
       		this.totalStudentsOne++;
          break;
        case 2:
          this.totalStudentsTwo++;
          break;
      }
      this.totalStudents++;
    },
  },
  created: function(){
  	this.totalStudents = this.students.length;
  }
}
</script>

<style>
#app {
  width:100%;
}
</style>
