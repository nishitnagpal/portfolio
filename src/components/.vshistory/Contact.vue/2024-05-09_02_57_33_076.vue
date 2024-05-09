<script>
import { reactive } from 'vue'
import { useVuelidate } from '@vuelidate/core'
import { required, email } from '@vuelidate/validators'

export default {
  setup () {
    const state = reactive({
        name: '',
        email: '',
        message: '',
        submitted: false,
        showThankYou: false
    })
    const rules = {
        name: { required }, // Matches state.name
        email: { required, email }, // Matches state.email
        message: { required } // Matchess this.message
    }

    const v$ = useVuelidate(rules, state)
     
    const handleSubmit = () => {
        console.log('form submit');

        // Assuming v$.value.$validate() returns a promise
        v$.value.$validate().then(result => {
            if (!result) {
                // If there are errors in the form, show an alert indicating that the form is invalid
                console.log('The form has errors');
                return;
            }

        // If the form is valid, perform some action with the form data
        console.log('Form submitted successfully');

        // Log form data
        console.log('Name:', state.name);
        console.log('Email:', state.email);
        console.log('Message:', state.message);

        // Show thank you message and reset form fields
        state.submitted = true
        state.showThankYou = true
        resetForm();

        // Hide thank you message after a few seconds
        setTimeout(() => {
            state.showThankYou = false;
            }, 3000); // Change 3000 to the desired duration in milliseconds (e.g., 3000 for 3 seconds)
        }).catch(error => {
            // Handle any errors that occur during validation
            console.error('Validation failed:', error);
        });
    }
    const resetForm = () => {
        state.name = ''
        state.email = ''
        state.message = ''
    }
    return { state, handleSubmit }
  }
}
</script>

ChatGPT

<template>
    <div class="container">
        <div class="form">
            <p>
                <span class="first-two-lines">
                    With a strong desire in frontend development and a passion for
                    creating innovative and user-friendly websites, I am excited about
                    the possibility of contributing to your team. <br />
                </span>
                <br />
                Currently, I'm seeking new job opportunities, so I would welcome the
                chance to discuss how my skills and expertise align with the needs
                of your team.
            </p>
            <div>
            <!--<div v-if="!state.submitted">-->
                <form @submit.prevent="handleSubmit">

                    <label for="name" class="custom-label">Name:</label>
                    <input type="text" id="name" placeholder="Enter your name" required v-model="state.name">
                    <span class="asterisk_input"> </span> <br>

                    <label for="email" class="custom-label">Email:</label>
                    <input type="email" id="name" placeholder="Enter valid email" required v-model="state.email">
                    <div v-if="emailError" class="error"> {{emailError}} </div>
                    <span class="asterisk_input"> </span> <br>

                    <label for="message" class="custom-label">Message:</label>
                    <textarea type="text" id="message" placeholder="Message" required v-model="state.message"> </textarea>
                    <span class="asterisk_input"> </span> <br>

                    <div class="submit">
                        <button type="submit" v-if="!state.submitted">Submit</button>
                    </div>
                </form>
            </div>
            <div class="thank-you-message" v-if="state.submitted && state.showThankYou">
                <p>Thank you for your valuable feedback!</p>
            </div>
        </div>
        <div class="socials">
            <h3></h3>
            <p>
                <article>
                    <img alt="location logo" src="./images/location.svg" /> <span class="description"> Bochum, Germany </span> <br>
                </article>
                <article>
                    <img alt="phone logo" src="./images/phone.svg" /> <!-- + <img alt="whatsapp logo" src="./images/whatsapp.svg" />--> <span class="description">  +4917637365466 </span> <br>
                </article>
                <article>
                    <img alt="Email logo" src="./images/email.svg" />
                    <a href="mailto:nshtngpl@gmail.com" rel="noopener noreferrer" target='_blank'> nshtngpl@gmail.com </a> <br>
                </article>
                <article>
                    <img alt="linkedin logo" src="./images/linkedin.svg" />
                    <a href="https://www.linkedin.com/in/nishitnagpal" target="_blank" rel="noopener noreferrer"> linkedin.com/in/nishitnagpal </a> <br>
                </article>
                <article>
                    <img alt="Github logo" src="./images/github.svg" />
                    <a href="https://github.com/nishitnagpal" target="_blank" rel="noopener noreferrer"> github.com/nishitnagpal </a> <br>
                </article>
             </p>
        </div>
    </div>
</template>

<style scoped>
/*
.form {
  position: relative;
}
*/

.thank-you-message {
  position: absolute;
  bottom: 4.7em;
  left: 10em;
  background-color: #42b883;
  padding: 10px;
  border-radius: 25px;
  display: block;
}

.thank-you-message p {
  color: black;
}

.thank-you-message.show {
  display: block;
}

.custom-label {
    font-size: 16px;
    font-family: Arial, sans-serif;
}
    
.container {
   display: grid;
   grid-template-columns: repeat(2, minmax(0, 1fr));
   top: 4em;
}

.container p {
   font-size: 15px;
}

.form{
    padding-right:25px;
}

.socials{
    display: block;
    padding: 3em 0em 0em 8em;
    font-size: 18px;
    z-index: -1;
}

.socials h3{
    text-align: right;
    padding-right: 30px;
}

a, .white {
   text-decoration: none;
   color: white;
   padding-left: 1em;
   transition: font-size ease-in-out 0.3s;
}

.contrast a, .black{
    color: black;
}

@media (hover: hover) {
   .socials a:hover {
      font-size: 17px;
      cursor: pointer;
   }
}

.socials img {
   position: relative;
   height: 38px;
   width: auto;
   vertical-align: middle;
   padding: 0px 0 20px 0px;
   display: inline-block;
}

.socials article{
    padding-bottom: 30px;
}

form {
    max-width: 500px;
    width: 500px;
    height: 350px;
    max-height: 500px;
    border: 1px solid #42b883;
    padding: 20px 20px 0px 10px;
    margin: 30px 20px 50px 20px;
    border-radius: 0.5rem;
}

.asterisk_input::after {
    content:" *required"; 
    color: red;
    position: absolute;  
    font-size: 12px; 
}

.description{
    padding-left: 1em;
}

input, textarea {
    display: block;
    width: 100%;
}
#message{
    max-height: 100px;
    height: 100px;
}

input::placeholder{
    position: absolute;
    top: 0px;
}

button{
    background: #42b883;
    border:0;
    padding: 1em;
    margin-top: 0px;
    color: #252526;
    border-radius: 20px;
}

.submit{
    text-align: right;
}

.first-two-lines{
    color: #42b883;
}

.font-change p, .font-change label, .font-change .submit button, .font-change .socials {
    font-size: 20px;
}

.font-change form{
    height: 400px;
    padding: 10px 20px 0px 20px;
    margin: 30px 20px 50px 20px;
}

.form p{
    margin: 0;
}

</style>

