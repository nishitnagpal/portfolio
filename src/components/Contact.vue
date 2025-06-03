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
    return { state, handleSubmit}
  },
  data() {
    return {
        isHamburgerMenuOpen: false,
    }
  },      
  computed: {
    toggleHamburgerMenu() {
      this.isHamburgerMenuOpen = !this.isHamburgerMenuOpen;
    },
  },
}
</script>

<template>
<div class="parent_logo-container">  
    <div class="hamburger-container" @click="toggleHamburgerMenu">
            <img src="./images/hamburger.svg" alt="Hamburger Menu" class="hamburger-icon">
    </div>

    <div v-if="isHamburgerMenuOpen" class="hamburger-menu">
        <ul>
            <li><RouterLink to="/"> Home </RouterLink></li>
            <li><RouterLink to="/Projects">Projects</RouterLink></li>
            <li><RouterLink to="/About">About</RouterLink></li>
            <li><RouterLink to="/Contact">Contact</RouterLink></li>
            <li><a href="Resume.pdf" target="_blank" rel="noopener">Resume</a></li>
        </ul>
    </div>
    <div class="container">
        <div class="form">
            <p>
                <span class="first-two-lines">
                    Excited to collaborate or have a project in mind? Whether it's unlocking data insights, crafting innovative solutions, or building seamless web experiences, let's connect and create something remarkable! <br />
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
                <!--
                <article>
                    <img alt="location logo" src="./images/location.svg" /> <span class="description"> Bochum, Germany </span> <br>
                </article>
                <article>
                    <img alt="phone logo" src="./images/phone.svg" /> <span class="description">  +917044081133 </span> <br>
                </article>
                -->
                <article>
                    <img alt="whatsapp logo" src="./images/whatsapp.svg" /> <span class="description">  +91-9163409749 </span> <br>
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
</div>    
</template>

<style scoped>

@import '@/assets/main.css';
@import '@/components/Navbar.css';

/*
.form {
  position: relative;
}
*/

.parent_logo-container {
    width: 100%;
    display: flex;       
    justify-content: flex-end; 
    box-sizing: border-box;
    /*align-items: center;*/
}


.thank-you-message {
  position: absolute;
  background-color: #42b883;
  padding: 1em;
  border-radius: 10px;
  margin-top: 1em;
  color: black;  
  bottom: 6em;
  left: 10em;
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
    color: #42b883;
}
    
.container {
   display: grid;
   grid-template-columns: repeat(2, minmax(0, 1fr));
   /*margin: 4em;*/
   gap: 30px;

   padding: 0 1em;
   margin-top: 2em;
}

.container p {
   font-size: 15px;
}

.form{
    /*
    padding-right:25px;
    padding-top: 2.5em;
    */
    max-width: 100%;

    padding: 2em 1em;
}

.socials{
    display: block;
    /*padding: 3em 0em 0em 8em;*/
    font-size: 18px;
    z-index: -1;

    padding: 3em 0 0 2em;
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

.contrast-change a, .black{
    color: black;
}

@media (hover: hover) {
   .socials a:hover {
      font-size: 17px;
      cursor: pointer;
    }
}

.socials img {
   height: 38px;
   width: auto;
   vertical-align: middle;
   padding: 0px 0 20px 0px;

   /*
   display: inline-block;
   position: relative;
   */
}

.socials article{
    padding-bottom: 20px;
}

form {
    max-width: 500px;
    /*
    width: 500px;
    height: 350px;
    max-height: 500px;
    */
    border: 1px solid #42b883;
    /*padding: 20px 20px 0px 10px;*/
    margin: 30px 20px 50px 20px;
    border-radius: 0.5rem;

    padding: 1.5em;
    background-color: #f9f9f9; /* Subtle background for contrast */
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
    padding: 10px;
    margin-bottom: 1em;
    font-size: 16px;
    border-radius: 5px;
    border: 1px solid #ccc;
    box-sizing: border-box;
}

#message{
    max-height: 100px;

    /*height: 100px;*/
}

input::placeholder{
    vertical-align: center;
}

button{
    background: #42b883;
    border:0;
    padding: 1em;
    margin-top: 0px;
    color: #252526;
    border-radius: 20px;

    cursor: pointer;
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
    margin-left: 20px;
}

/* Hamburger Menu */

.hamburger-container {
  display: none; /* Hide hamburger menu on larger screens */
  position: fixed;
  margin: 0;
}

.hamburger-icon {
  width: 30px;
  height: 30px;
  cursor: pointer;
}

.hamburger-menu{
    position: fixed; /* Fullscreen menu */
    top: 4rem;
    width: 100%;
    height: 100%;
    background-color: rgba(163, 228, 198, 0.95); /* Semi-transparent black background */
    display: flex; /* Use flexbox for centering */
    flex-direction: column; /* Stack items vertically */
    align-items: center; /* Center items horizontally */
    justify-content: center; /* Center items vertically */
    z-index: 9999; /* Make sure it's above everything */
    transition: opacity 0.3s ease, visibility 0.3s ease; /* Smooth transition */    
}

.hamburger-menu ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.hamburger-menu ul li {
  margin: 0.5rem 0 2rem 1rem;
}

.hamburger-menu ul li a {
  color: black;
  text-decoration: none;
  font-size: 1.2rem;
  transition: color 0.3s ease;
}

.hamburger-menu ul li a:hover {
  color: #ffd700; /* Highlight color on hover */
}


@media (max-width: 768px) {
    /* Adjust the layout for tablets and smaller screens */
    .container {
        grid-template-columns: 1fr; /* Stack the form and socials vertically */
        gap: 20px;
        margin-top: 2em;
        padding: 0;
    }

    .socials {
        /*
        padding-left: 1em; // Adjust padding for mobile view 
        padding-right: 1em;
        */
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        padding: 1em 0;
        text-align: center;
        border-top: 1px solid #42b883;
        flex-wrap: wrap;
    }

    .form {
        max-width: 90%; /* Allow form to take more width on smaller screens */
        padding-right: 10px;
        padding-bottom: 0px;
    }

    .form p {
        font-size: 14px; /* Make the text size smaller on mobile */
    }

    input, textarea {
        padding: 10px;
        font-size: 14px;
    }

    .submit button {
        font-size: 14px;
        padding: 0.8em 1.5em; /* Adjust button padding on small screens */
    }

    .socials article {
        padding: 1em; /* Adjust padding between social items */
        flex: 1 1 120px; /* Flex items with minimum width */
        text-align: center; /* Center-align each item */
        display: flex;
        align-items: center;
    }

    .socials img {
        height: auto;
        width: 30px;
    }
    
    .socials a {
        display: none;
    }

    .socials .description{
        display: none;
    }

    .hamburger-container {
        display: block; /* Show hamburger menu on smaller screens */
    }
    .navbar.isHamburgerMenuOpen nav {
        display: block;
    }
}

@media (max-width: 480px) {
    /* Adjust for smaller devices like mobile phones */
    .container {
        grid-template-columns: 1fr; /* Stack content vertically */
        padding: 0 1em; /* Add some padding to the sides */
    }

    .socials {
        display: none;
        padding: 0;
        border: 2px solid red;
    }

    .form {
        max-width: 100%; /* Full width form */
        /*
        padding-right: 10px;
        padding-left: 10px;
        */

        padding: 1em;
    }

    .form p {
        font-size: 12px; /* Make text even smaller */
    }

    input, textarea {
        font-size: 14px;
    }

    .submit button {
        font-size: 16px;
        padding: 0.7em 1.2em; /* Adjust button padding on mobile */
    }

    .socials img {
        height: 28px; /* Resize social icons on mobile */
    }

    .socials article {
        padding: 0px; /* Adjust padding */
        margin: 0;
    }

    .thank-you-message { 
        bottom: 6em;
        left: 5em;
    }
}

@media (max-width: 375px) {

    .thank-you-message { 
        bottom: 6em;
        left: 4em;
    }

}

@media (max-width: 325px) {

.thank-you-message { 
    bottom: 0;
    left: 2em;
}

}

</style>

