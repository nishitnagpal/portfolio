<script>

import { state } from "@/components/State.js";
/*
export default {
    beforeCreate: function () {
        document.body.className = 'Home';
    }
}
*/

export default {
    data() {
        return {
            //contrastToggleValue: false,
            //fontToggleValue: false, 
            isDropdownVisible: false,
            isHamburgerMenuOpen: false,
            titles: ["DATA SCIENTIST", "DATA ANALYST", "WEB DEVELOPER", "UI ENGINEER", "UX DESIGNER"],
            currentTitleIndex: 0,
            currentTitle: "MECHATRONICS ENGINEER", // Default or initial title
            intervalId: null, // To store the interval ID
            isMobile: false, // Track if it's mobile view
        };
    },
        
    watch: {
        contrastToggleValue(newValue) {
            if (newValue) {
                document.body.classList.add('contrast-change');  // Apply contrast-change class to body
            } else {
                document.body.classList.remove('contrast-change');  // Remove contrast-change class from body
            }
        },
        fontToggleValue(newValue) {
            if (newValue) {
                document.body.classList.add('font-change');  // Apply font-change class 
            } else {
                document.body.classList.remove('font-change');  // Remove font-change class
            }
        },
    },
    
    methods: {
        toggleDropdown() {
            const dropdownMenu = document.getElementById("dropdownMenu");
            if (!dropdownMenu) return;
            dropdownMenu.classList.toggle("show");
            this.isDropdownVisible = dropdownMenu.classList.contains("show");
        },
        toggleHamburgerMenu() {
            this.isHamburgerMenuOpen = !this.isHamburgerMenuOpen;
        },    
        rotateTitle() {
            // Update the current title
            this.currentTitle = this.titles[this.currentTitleIndex];
            // Move to the next title, or reset to the first title
            this.currentTitleIndex = (this.currentTitleIndex + 1) % this.titles.length;
        },
        checkIfMobile() {
            this.isMobile = window.innerWidth <= 768; // Set mobile view at max 768px
        }
    },

    mounted() {
        this.checkIfMobile(); // Check on load
        window.addEventListener('resize', this.checkIfMobile); // Update on window resize
            
        // Start rotating titles in regular intervals
        this.intervalId = setInterval(() => {
            this.rotateTitle();
        }, 1000);
    },

    beforeDestroy() {
        // Clear the interval when component is destroyed to prevent memory leaks
        if (this.intervalId) {
            clearInterval(this.intervalId);
        }
        window.removeEventListener('resize', this.checkIfMobile);
    },

    computed: {
        contrastToggleValue: {
            get() {
                return state.contrastToggleValue;
            },
            set(value) {
                state.contrastToggleValue = value;
            },
        },
        fontToggleValue: {
            get() {
                return state.fontToggleValue;
            },
            set(value) {
                state.fontToggleValue = value;
            },
        },
        contrastLabel() {
            return this.contrastToggleValue ? "Light mode" : "Dark mode";
        },
        fontLabel() {
            return this.fontToggleValue ? "Big Font" : "Small Font" ;
        },
    },
};

</script>

<template>
<!-- Logos -->
<!--<div :class="{ 'font-change': fontToggleValue }">-->
<div class = "parent_logo-container">
    <!-- Hamburger Icon -->
    <div class="hamburger-container" @click="toggleHamburgerMenu">
        <img src="./images/hamburger.svg" alt="Hamburger Menu" class="hamburger-icon">
    </div>

    <div v-if="isHamburgerMenuOpen" class="hamburger-menu">
      <ul>
        <li><RouterLink to="/Projects">Projects</RouterLink></li>
        <li><RouterLink to="/About">About</RouterLink></li>
        <li><RouterLink to="/Contact">Contact</RouterLink></li>
        <li><a href="Resume.pdf" target="_blank" rel="noopener">Resume</a></li>
      </ul>
    </div>

    <div class="logo-container">
        <div class="dropdown" id="dropdownContainer">
            <img src="./images/settings.svg" alt="Settings for Dropdown Menu Logo" @click="toggleDropdown()">
            <div class="dropdown-content" id="dropdownMenu">
                <div class="menu-item">
                    <label class="toggle-switch">   
                        <input type="checkbox" v-model="contrastToggleValue" />
                        <img v-bind:src="contrastToggleValue ? './toggleon.svg' : './toggleoff.svg'" alt="Toggle Image">
                    </label>
                    <!--<img src="./images/toggle-on.svg" alt="Toggle-0n Icon">-->
                    <span class="styled-text">{{ contrastLabel }}</span>
                </div>

                <div class="menu-item">
                    <!--<label class="toggle-switch" @click="toggleFont">-->
                    <label class="toggle-switch">
                        <input type="checkbox" v-model="fontToggleValue" />
                        <img v-bind:src="fontToggleValue ? './toggleon.svg' : './toggleoff.svg'" alt="Toggle Image">
                    </label>
                    <!--<img src="./images/toggle-on.svg" alt="Toggle-0n Icon">-->
                    <span class="styled-text">{{ fontLabel }}</span>
                </div>
            </div>
        </div>
                
        <template v-if="isDropdownVisible">
            <div class="logo-text">  &nbsp;  &nbsp;  &nbsp;  &nbsp;  &nbsp;  &nbsp;  &nbsp;  &nbsp;  &nbsp;  &nbsp;  &nbsp; &nbsp; </div>
        </template>

        <template v-else>
            <img src="./images/contrast.svg" alt="Contrast Change Logo" class="logo1">
            <img src="./images/fontincrease.svg" alt="Font Change Logo" class="logo1">
        </template>
    </div>
</div>
    <!-- Hamburger Menu (Mobile View) -->
    <navbar-component v-if="isMobile"></navbar-component>

<div class="container">
    <div class="greetings logo">
        <h1> NISHIT NAGPAL </h1>
        <h3>{{ currentTitle }}</h3>
        <p>
            Hi, <br />
            My background in mechanical engineering and mechatronics uniquely positions me to bridge the gap between complex data and intuitive design. <br /><br />
            I approach problems from a holistic perspective, considering both the technical intricacies and the human-centric aspects of the solution.
        </p>
        <div class="footer-socials">
            <a href="https://www.linkedin.com/in/nishitnagpal" target="_blank" rel="noopener noreferrer">
                <img alt="linkedin logo" src="./images/linkedin.svg" />
            </a>
            <a href="https://github.com/nishitnagpal" target="_blank" rel="noopener noreferrer">
                <img alt="Github logo" src="./images/github.svg" />
            </a>
            <a href="mailto:nshtngpl@gmail.com" rel="noopener noreferrer" target='_blank'>
                <img alt="Email logo" src="./images/email.svg" />
            </a>
        </div>
    </div>
    <div class="navbarbox1">
        <div class="box1">
            <img alt="Project icon" src="./images/projects.svg" width="50" height="50" />
            <h4><RouterLink to="/Projects">Projects</RouterLink></h4>
        </div>
        <div class="box2">
            <img alt="About icon" src="./images/about.svg" width="50" height="50" />
            <h4><RouterLink to="/About">About</RouterLink></h4>
        </div>
    </div>
    <div class="navbarbox2">
        <div class="box3">
            <img alt="Contact icon" src="./images/contact.svg" width="50" height="50" />
            <h4><RouterLink to="/Contact">Contact</RouterLink></h4>
        </div>
        <div class="box4">
            <img alt="Resume icon" src="./images/resume.svg" width="50" height="50" />
            <a href="Resume.pdf" target="_blank" rel="noopener"> <h4>Resume</h4> </a>
        </div>
    </div>
</div>
</template>

<style scoped>

@import '@/assets/main.css';

.container {
    display: grid;
    grid-template-columns: auto auto auto;
    /*margin-top: 4em;*/
}
.navbarbox1, .navbarbox2 {
    display: inline-block;
    margin-right: auto;
    margin-top: 2em;
}
.box1, .box2, .box3, .box4 {
    width: 200px;
    height: 130px;
    border: 1px solid #42b883;
    padding: 60px 10px 0px 10px;
    margin: 50px 20px 50px 20px;
    border-radius: 0.5rem;
    background-color: papayawhip;
    transition: transform 0.3s ease-in-out;
    text-align: center;
}

h1 {
    font-weight: 500;
    font-size: 2.8rem;
    position: relative;
    margin-bottom: 0px;
}

h3 {
    font-size: 1.8rem;
    margin-top: 0px;
    color: #42b883!important;
    margin-bottom: 0px;
}

h4 {
    font-size: 28px;
    margin-top: 0px;
    color: #42b883!important;
}

button {
    background-color: transparent;
    color: #42b883;
    border: 1px solid;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: 0.25rem;
    transition: transform 0.3s ease-in-out;
}

.logo img {
    position: relative;
    height: 35px;
    width: auto;
    vertical-align: middle;
    padding: 0px 30px 0px 0px;
    display: inline-block;
}

.footer-socials{
    display: flex;
    justify-content: flex-start;
}

a,
.green {
    text-decoration: none;
    color: hsla(160, 100%, 37%, 1);
    transition: transform 0.3s ease-in-out;
    padding: 3px;
}

p{
    text-align: justify;
    font-size: 16px;
}

.greetings{
    display: inline-block;
    padding: 2rem 1rem 0;
    /*padding: 100px 100px 0px 0px;*/
    vertical-align: middle;
    /*margin-left: 50px;*/
    margin: 2rem 0 0 2rem; 
    max-width: 90%;
    box-sizing: border-box;
}

.greetings h1,
.greetings h3 {
    text-align: left;
}

    /*New css*/
    /*
    .navbar{
    display: flex;
    float: right;
    font-size: 20px;
    height: 2.9rem;
    align-items: center;
    justify-content: center;
    /*
    display: flex;
    flex-flow: wrap;
    justify-content: space-evenly;
    position: sticky; 
    //  
    }
    */
.logo1, .dropdown img {
    height: auto;
    width: 30px;
    padding-right: 20px;
}

.dropdown img {
    margin-top: 6px;
}

.parent_logo-container {
    width: 100%;
    display: flex;       
    justify-content: flex-end; 
    box-sizing: border-box;
    /*align-items: center;*/
}

.logo-container {
    position: relative;
    background-color: #42b883;
    border-radius: 25px;
    height: 2.7rem;
    /*--logo-cotainer-width: auto;*/
    width: auto;
    /*padding-left: 20px;*/
    /*margin-right: 0px;*/
    padding: 0 20px; 
    margin: 1em 0 0 0;
    display: inline-block;
    align-items: center;
    /*justify-content: flex-end;
    top: 10px;
    right: 20px;*/   
}

/* Initially hide the dropdown menu */
#dropdownMenu {
    display: none;
}

/* Show the dropdown menu when the .show class is applied */
#dropdownMenu.show {
     display: block;
}


#dropdownContainer {
    position: relative; /* Set position relative for the container */
    display: inline-block; /* Ensure container width matches content width */
}

#dropdownContainer img {
    cursor: pointer; /* Change cursor to pointer for better UX */
}

.dropdown {
    position: relative;
    display: inline-block;
}


.dropdown-content {
    display: none;
    background-color: #252526;
    color: white;
    /*
    top: 100%;
    left: 0;
    */
    border-radius: 25px;
    /*width: 140px;*/
    width: auto;
    padding: 0.3rem;
    margin-top: 1px;
}

.dropdown-content a {
    color: #42b883;
    display: block;
}
        /*
    .option1 img {
    position: absolute;
    width: 40px;
    height: 30px;
    left: 10px;
    padding: 0;
    }

    .option1 {
    display: flex;
    align-items: center;
    }
    */
.toggle-switch {
    position: absolute;
    display: inline-block;
    cursor: pointer;
    width: 40px;
    height: 30px;
    padding: 0;
}

.styled-text {
    font-size: 16px;
    margin-top: 8px;
    margin-left: 50px;
}


.toggle-switch input {
    display: none; /* Hide the actual checkbox */
}

.menu-item {
    display: flex;
    align-items: center;
}

.toggle-switch img {
    position: absolute;
    width: 40px;
    height: 30px;
    left: 10px;
    padding: 0;
}

.logo-text {
    margin: 0 5px 0 0;
    font-weight: bold;
}

/*Font change css*/

/*
.font-change .container p{
    font-size: 25px!important;
}



.font-change .greetings {
    padding: 2rem 1rem 0!important;
    margin: 2rem 0 0 2rem;
}
*/

/* Font change css*/

.hamburger-container {
  display: none; /* Hide hamburger menu on larger screens */
  position: fixed;
  margin: 25px 0 0 0;
}

.hamburger-icon {
  width: 30px;
  height: 30px;
  cursor: pointer;
}
/*
.hamburger-menu {
  position: fixed;
  top: 4rem; 
  right: 1rem; 
  background-color: #87a195;
  border-radius: 8px;
  padding: 1rem;
  z-index: 10;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
  width: 100%;
  height: 100%;
}
*/

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

@media (hover: hover) {
    button:hover {
        transform: scale(1.2);
        cursor: pointer;
    }

    .logo img:hover {
        transform: scale(1.2);
        cursor: pointer;
    }

    .box1:hover, .box2:hover, .box3:hover, .box4:hover {
        transform: scale(1.2);
        cursor: pointer;
    }
}

/* Adjustments for laptop screens (1024px) */
@media (max-width: 1024px) {
    .greetings {
        padding: 1rem 0.5rem 0; 
        margin-left: 1rem; 
        text-align: center; 
    }
    .greetings p{
        font-size: 16.5px;    
    }
    .font-change .container p{
        font-size: 18px!important;
    } 
}

@media (min-width: 1440px) {
    .greetings {
        padding: 1rem 0.5rem 0; 
        margin-left: 1rem; 
        text-align: center; 
    }
    .greetings p{
        font-size: 22px;    
    }
    .font-change .container p{
        font-size: 25px!important;
    } 
}

/* Hide the navbarboxes and responsiveness for tablets */
@media (max-width: 768px) {
    .navbarbox1, .navbarbox2 {
        display: none;
    }

    .container {
        display: block;
        padding: 20px;
    }

    .greetings {
        padding: 40px 20px;
        margin-left: 0;
    }
    
    .logo-container {
        position: fixed;
        top: 10px;
        left: 40px;
    }

    .logo img {
        width: 20px;
    }

    .logo1, .dropdown img {
        height: auto;
        width: 30px;
    }
    .font-change .container p{
        font-size: 20px!important;
    }
    .hamburger-container {
        display: block; /* Show hamburger menu on smaller screens */
    }

    .navbar nav {
        display: none; /* Hide regular nav links on small screens */
    }

    /* Show hamburger menu when it's clicked */
    .navbar.isHamburgerMenuOpen nav {
        display: block;
    }
}

@media (max-width: 425px) {
    .greetings{
        margin-top: 2em;
    }

    .logo-container img{
        width: 20px;
        padding-right: 10px;
    }
    .logo-container{
        height: 30px;
        width: 90px;
    }
    .dropdown-content {
        border-radius: 25px;
        width: 110px;
    }
    .styled-text{
        font-size: small;
        padding: 0;
        margin-left: 30px;
    }
    .toggle-switch img {
        position: absolute;
        width: 20px;
        height: 20px;
        left: 0px;
        padding: 0;
    }
}

@media (max-width: 375px) {
    .container{
        margin: 0;
        padding: 0;
    }

    .greetings p{
        font-size: 12px;
    }

    .greetings h1{
        font-size: 28px;
    }

    .greetings h3{
        font-size: 18px;
    }

    .greetings{
        margin-top: 4rem;
    }

    .logo-container img{
        width: 20px;
        padding-right: 10px;
    }
    .logo-container{
        height: 30px;
        width: 90px;
    }
    .dropdown-content {
        border-radius: 25px;
        width: 110px;
    }
    .styled-text{
        font-size: small;
        padding: 0;
        margin-left: 30px;
    }
    .toggle-switch img {
        position: absolute;
        width: 20px;
        height: 20px;
        left: 0px;
        padding: 0;
    }
    .font-change .container p{
        font-size: 15px!important;
    }
    .footer-socials img{
        width: 20px;
    }
}


</style>



