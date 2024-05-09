<script>
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
<!-- Logos -->
<div class="logo-container">
    <div class="dropdown" id="dropdownContainer">
        <img src="./images/settings.svg" alt="Settings for Dropdown Menu Logo" @click="toggleDropdown()">
         <div class="dropdown-content" id="dropdownMenu">
            <div class="menu-item">
                <label class="toggle-switch" @click="toggleContrast">
                    <input type="checkbox" v-model="contrastToggleValue">
                    <img v-bind:src="contrastToggleValue ? './toggleon.svg' : './toggleoff.svg'" alt="Toggle Image">
                </label>
                <!--<img src="./images/toggle-on.svg" alt="Toggle-0n Icon">-->
                <span class="styled-text">Contrast</span>
            </div>

            <div class="menu-item">
                <label class="toggle-switch" @click="toggleFont">
                    <input type="checkbox" v-model="fontToggleValue">
                    <img v-bind:src="fontToggleValue ? './toggleon.svg' : './toggleoff.svg'" alt="Toggle Image">
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

<div class="container">
    <div class="greetings logo">
        <h1> NISHIT NAGPAL </h1>
        <h3> FRONTEND DEVELOPER </h3>
        <p>
            Self-taught frontend developer passionate about crafting immersive digital experiences. My background in mechanical engineering and mechatronics uniquely positions me to approach frontend development from a holistic perspective, considering both the technical intricacies and the human-centric aspects of design.
        </p>

        <a href="https://nishitnagpal.github.io/cv/" target="_blank" rel="noopener noreferrer">
            <button> Know Me </button>
        </a>
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
    
.container {
    display: grid;
    grid-template-columns: 700px auto auto;
    margin-top: 4em;
}
.navbarbox1, .navbarbox2 {
    display: inline-block;
    margin-right: auto;
}
.box1, .box2, .box3, .box4 {
    width: 100%;
    height: 130px;
    border: 1px solid #42b883;
    padding: 60px 10px 0px 10px;
    margin: 50px 20px 50px 20px;
    border-radius: 0.5rem;
    background-color: papayawhip;
    transition: transform 0.3s ease-in-out;
    text-align: center;
    max-width: 400px;
    max-height: 260px;
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
    padding: 0px 0px 0px 10px;
    display: inline-block;
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
    padding: 100px 100px 0px 0px;
    vertical-align: middle;
    margin-left: 50px;
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

.logo-container {
    position: absolute;
    background-color: #42b883;
    border-radius: 25px;
    height: 2.7rem;
    --logo-cotainer-width: auto;
    padding-left: 20px;
    margin-right: 50px;
    display: flex;
    align-items: center;
    top: 10px;
    right: 20px;
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
    position: absolute;
    background-color: #252526;
    color: white;
    top: 100%;
    left: 0;
    border-radius: 25px;
    width: 140px;
    padding-bottom: 10px;
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

.font-change .container p{
    font-size: 20px!important;
}

.font-change .greetings {
    padding: 60px 100px 0px 0px!important;
}

/* Font change css*/

/*Contrast change css*/
.contrast body {
    background-color: white;
    color: #252526;
}
/*Contrast change css*/

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

@media (min-width: 1024px) {
    .greetings h1,
    .greetings h3 {
        text-align: left;
    }
}
</style>