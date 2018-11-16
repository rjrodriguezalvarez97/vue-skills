<template>
    <div class="hello">
        <div class="holder">

            <form @submit.prevent="addSkill">
                <input type="text" placeholder="Enter a skill you have.." v-model="skill" v-validate="'min: 5'" name="skill">
                <p class="alert" v-if="errors.has('skill')"> {{ errors.first('skill') }} </p>
                <p class ="danger" v-if="notValid"> Your input is not valid</p>
            </form>

            <ul>
            <li v-for="(data, index) in skills" :key='index'> {{data.skill}} </li>
            </ul>
            <!-- <p v-if="skills.length >= 1"> You have more than 1 skills </p>
            <p v-else> You have less than or equal to 1 skill </p> -->

        <p> These are the skills that you possess </p>
        </div>
    </div>
</template>

<script>
export default {
name: 'Skills',
    data() {
        return {
            skill: '',//binded to text input
            skills: [
                { "skill": "Vue.js"},
                { "skill": "Frontend Developer"}
            ],
            notValid: false
        }
    },
    methods: {
        addSkill() {
            this.$validator.validateAll().then( (result) => {
                if(result){
                    this.skills.push({skill: this.skill});
                    this.skill = '';
                } else{
                    this.notValid = true;
                }
            })

        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<!--
// <style  src="./Skills.css" scoped>

// </style>
-->
<style scoped>

    .holder {
        background: #fff;
    } 

    ul {
        margin: 0;
        padding: 0;
        list-style-type: none;
    }
  
    ul li {
        padding: 20px;
        font-size: 1.3em;
        background-color: #E0EDF4;
        border-left: 5px solid #3EB3F6;
        margin-bottom: 2px;
        color: #3E5252;
    }

    p {
        text-align:center;
        padding: 30px 0;
        color: gray;
    }

    .container {
        box-shadow: 0px 0px 40px lightgray;
    }
    input {
        width: calc(100% - 40px);
        border: 0;
        padding: 20px;
        font-size: 1.3em;
        background-color: #323333;
        color: #687F7F;
    }
    .alert {
        background: #fdf2ce;
        font-weight: bold;
        display: inline-block;
        padding: 5px;
        margin-top: -20px;
    }
    .danger {
        background: #f46e42;
        font-weight: bold;
        padding: 20px;
        width: calc(100% - 40px);
        height: 20px;
    }

</style>


