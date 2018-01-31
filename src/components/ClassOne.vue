<template>
  <div class="col-sm-6 col-xs-12">
    <h1>Class #1</h1>
    <ul class="list-group">
      <li class="list-group-item" v-for="(student, index) in students">{{ student }} <br> <button class="btn btn-info" @click="returnBack(student, index)">Return to School</button> <button class="btn btn-success" @click="moveToClassTwo(student, index)">Move to #2</button> <button class="btn btn-danger" @click="removeStudent(student, index)">Leave School</button></li>
    </ul>
  </div>
</template>

<script>
import { bus } from '../main';

export default {
  props: ['student'],
	data: function(){
  	return {
    	students: [],
    }
  },
  watch: {
  	student: function(student){
    	this.students.push(student);
    }
  },
  methods: {
  	returnBack: function(student, index){
    	this.students.splice(index, 1);
      this.$emit('return', student);
    },
    moveToClassTwo: function(student, index){
    	this.$emit('decrease', 1);
      this.$emit('increase', 2);
    	bus.$emit('is-moved-two', student);
      this.students.splice(index, 1);
    },
    removeStudent: function(student, index){
    	this.students.splice(index, 1);
      this.$emit('decrease', 1);
    },
    moved: function(student){
    	this.students.push(student);
    }
  },
  created: function(){
  	bus.$on('is-moved-one', this.moved);
  }
}
</script>

<style>

</style>
