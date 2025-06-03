<script>

import { state } from "@/components/State.js";

export default {
    data() {
        return {
            //contrastToggleValue: false,
            //fontToggleValue: false, 
            isDropdownVisible: false,
            //isHamburgerMenuOpen: false, 
        };
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
        }
    },
 
    methods: {  
      toggleDropdown() {
          var dropdownMenu = document.getElementById("dropdownMenu");
          if (!dropdownMenu) {
              return;
          }
          // Toggle a CSS class to control visibility
          dropdownMenu.classList.toggle("show");

          // Update the flag based on the visibility of the dropdown menu
          this.isDropdownVisible = dropdownMenu.classList.contains("show");
      },
      /*
      toggleHamburgerMenu() {
        this.isHamburgerMenuOpen = !this.isHamburgerMenuOpen;
        console.log("Hamburger menu clicked!");
      },
      */
    }
};
</script>

<template>
<div class="navbar">
    <nav>
        
        <!-- Hamburger Icon 
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
        -->
        

        <RouterLink to="/"> Home </RouterLink>
        <RouterLink to="/About"> About </RouterLink>
        <RouterLink to="/Projects"> Projects </RouterLink>
        <RouterLink to="/Contact"> Contact </RouterLink>
    </nav>
    
    <!-- Logos -->
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
</template>

<style scoped>
/* Import styles from Navbar.css */    
@import './Navbar.css';

nav a {
  float: left; /* Float the anchor elements (links) to the left */
  display: block; /* Display the links as block elements */
  color: white; /* Text color */
  text-align: center; /* Center align text within the links */
  margin: 0 5em 0 0; /* Padding to create space around the text */
  padding: 10px 1em 10px 1em; 
  text-decoration: none; /* Remove underline from links */
  transition: background-color 0.3s, color 0.3s; /* Add transition for smooth hover effect */
  font-size: 18px;
}

nav a:hover {
  background-color: #42b883; /* Background color on hover */
  cursor: pointer;
  border-radius: 10px;
}

nav a.router-link-exact-active{
   background-color: #FAFAD2;
   color: black;
   pointer-events: none;
   border-radius: 10px;
}

.contrast-change nav a {
   background-color: #FAFAD2;
   color: #252526;
}

.contrast-change nav a.router-link-exact-active {
    color: #FAFAD2;
    background-color: #252526;
} 

.contrast-change a:hover {
    background-color: #42b883;
}

</style>