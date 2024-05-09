<script>

import toggleonImage from '@/components/images/toggle-on.svg';
import toggleoffImage from '@/components/images/toggle-off.svg';

export default {
  data() {
    return {
        contrastToggleValue: true,
        fontToggleValue: true, // Initial value of the toggle switch
        isDropdownVisible: false
    };
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
      toggleContrast() {
          //console.log("Contrast toggle switch is:", this.contrastToggleValue)
              if (this.contrastToggleValue) {
              // Apply contrast mode (add 'contrast' class)
              document.documentElement.classList.add('contrast');
          } else {
              // Remove contrast mode (remove 'contrast' class)
              document.documentElement.classList.remove('contrast');
          }
             // console.log("Contrast mode is now:", document.documentElement.classList.contains('contrast') ? "ON" : "OFF");
      },
      toggleFont() {
          //console.log("Font toggle switch is:", this.fontToggleValue)
          if (this.fontToggleValue) {
              document.documentElement.classList.add('font-change');
          } else {
              document.documentElement.classList.remove('font-change');
          }
          // console.log("Contrast mode is now:", document.documentElement.classList.contains('font_increase') ? "ON" : "OFF");

      },
      mounted() {
          this.toggleDropdown();
          this.toggleContrast();
          this.toggleFont();
      }
  }
};
</script>

<template>
<div class="navbar">
        <nav>
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
                    <label class="toggle-switch" @click="toggleContrast">
                        <input type="checkbox" v-model="contrastToggleValue">
                        <img v-bind:src="contrastToggleValue ? 'toggleonImage' : 'toggleoffImage'" alt="Toggle Image">
                    </label>
                    <!--<img src="./images/toggle-on.svg" alt="Toggle-0n Icon">-->
                    <span class="styled-text">Contrast</span>
                </div>

                <div class="menu-item">
                    <label class="toggle-switch" @click="toggleFont">
                        <input type="checkbox" v-model="fontToggleValue">
                        <img v-bind:src="fontToggleValue ? '/toggle-on.svg' : '/toggle-off.svg'" alt="Toggle Image">
                    </label>
                    <!--<img src="./images/toggle-on.svg" alt="Toggle-0n Icon">-->
                    <span class="styled-text">Font</span>
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
   background-color: white;
   color: black;
   pointer-events: none;
   border-radius: 10px;
}

.contrast nav a {
   background-color: white;
   color: #252526;
}

.contrast nav a.router-link-exact-active {
    color: white;
    background-color: #252526;
} 

.contrast a:hover {
    background-color: #42b883;
}

</style>