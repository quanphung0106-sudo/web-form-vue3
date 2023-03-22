<template>
    <form @submit.prevent="handleSubmit">
        <label for="">Email</label>
        <input v-model="email" type="email" name="" id="" required>
        <label for="">Password</label>
        <input v-model="password" required type="password" name="" id="">
        <div v-if="passwordError">{{ passwordError }}</div>
        <label for="">Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

            <label for="">Skills</label>
            <input type="text" v-model="tempSkill" @keyup="addSkill">
            <div v-for="skill in skills" :key="skill" class="pill">
                {{ skill }}
                <span @click="deleteSkill(skill)">Delete</span>
            </div>
        <div class="terms">
            <input type="checkbox" v-model="terms" required name="checkbox" id="checkbox">
            <label for="checkbox" style="user-select: none;">Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Create an Account</button>
        </div>

        <!-- <div>
            <input id="quan" value="quan" type="checkbox" v-model="names">
            <label for="quan" style="user-select: none;">Quan Phung</label>
        </div>
        <div>
            <input id="mario" value="mario" type="checkbox" v-model="names">
            <label for="mario" style="user-select: none;">Mario</label>
        </div>
        <div>
            <input id="yoshi" value="yoshi" type="checkbox" v-model="names">
            <label for="yoshi" style="user-select: none;">Yoshi</label>
        </div> -->
    </form>

    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Terms: {{ terms }}</p>
    <!-- <p>Name: {{ names }}</p> -->
    <p>Skills: {{ skills }}</p>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: 'designer',
            terms: false,
            names: [],
            tempSkill: '',
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        addSkill (e) {
            if (e.key === "," && this.tempSkill) {
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ''
            }
        },
        deleteSkill(deleteSkill) {
            const newSkills = this.skills.filter(skill => skill !== deleteSkill)
            this.skills = newSkills
        },
        handleSubmit() {
            this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long'
            if (!this.passwordError) {
                
            }
        }
    }
}
</script>

<style scoped>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input,
select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
  }
  button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
  }
  .submit {
    text-align: center;
  }
  .error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
  } 
</style>