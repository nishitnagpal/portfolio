<script>
    import { ref, onMounted, reactive } from 'vue';
    import htmlImage from '@/components/images/html.svg';
    import cssImage from '@/components/images/css.svg';
    import typescriptImage from '@/components/images/typescript.svg';
    import javascriptImage from '@/components/images/javascript.svg';
    import reactImage from '@/components/images/react.svg';
    import vueImage from '@/components/images/vue.svg';
    import javaImage from '@/components/images/java.svg';
    import pythonImage from '@/components/images/python.svg';
    import gitImage from '@/components/images/git.svg';
    import matlabImage from '@/components/images/matlab.svg';
    import visualstudioImage from '@/components/images/visualstudio.svg';
    import csharpImage from '@/components/images/csharp.svg';
    import wordpressImage from '@/components/images/wordpress.svg';
    import phpImage from '@/components/images/php.svg';
    import mysqlImage from '@/components/images/mysql.svg';
    import autocadImage from '@/components/images/autocad.svg';
    import solidworksImage from '@/components/images/solidworks.svg';
    import unityImage from '@/components/images/unity.svg';
    import jiraImage from '@/components/images/jira.svg';
    import powerBIImage from '@/components/images/powerbi.svg';
    import tableauImage from '@/components/images/tableau.svg';
    import machinelearningImage from '@/components/images/machinelearning.svg';
    import tensorflowImage from '@/components/images/tensorflow.svg';
    import scikitlearnImage from '@/components/images/scikitlearn.svg';

export default {
    setup() {
    const imagesData = ref([
            {
                src: machinelearningImage,
                description: 'ML'
            },
            {
                src: tensorflowImage,
                description: 'Tensor Flow'
            },
            {
                src: scikitlearnImage,
                description: 'Scikit-Learn'
            },
            {
                src: mysqlImage,
                description: 'mySQL'
            },
            {
                src: pythonImage,
                description: 'Python'
            },
            {
                src: powerBIImage,
                description: 'PowerBI'
            },
            {
                src: tableauImage,
                description: 'Tableau'
            },
            
            {
                src: javascriptImage,
                description: 'JavaScript'
            },
            {
                src: typescriptImage,
                description: 'TypeScript'
            },
            {
                src: reactImage,
                description: 'React'
            },
            {
                src: vueImage,
                description: 'Vue'
            },
            {
                src: htmlImage,
                description: 'HTML5'
            },
            {
                src: cssImage,
                description: 'CSS3'
            },
            {
                src: wordpressImage,
                description: 'WordPress'
            },
            {
                src: phpImage,
                description: 'PHP'
            },
            {
                src: javaImage,
                description: 'Java'
            },
            {
                src: csharpImage,
                description: 'C#'
            },
            {
                src: gitImage,
                description: 'Git'
            },
            {
                src: visualstudioImage,
                description: 'Visual Studio'
            },
            {
                src: autocadImage,
                description: 'AutoCAD'
            },
            {
                src: solidworksImage,
                description: 'Solidworks'
            },
            {
                src: unityImage,
                description: 'Unity'
            },
            {
                src: jiraImage,
                description: 'Jira'
            },
            {
                src: matlabImage,
                description: 'MATLAB'
            }
    ]);

    const isPaused = ref(false);

    const pauseAnimation = () => {
      isPaused.value = true;
    };

    const resumeAnimation = () => {
      isPaused.value = false;
    };

    return {
      imagesData,
      isPaused,
      pauseAnimation,
      resumeAnimation,
    };

    },
    data() {
        return {
            isHamburgerMenuOpen: false,
        }    
    },   
    methods: {
        toggleHamburgerMenu() {
            this.isHamburgerMenuOpen = !this.isHamburgerMenuOpen;
        },
    },  
};
</script>

<template>
    <div class = "parent_logo-container">
    <!-- Hamburger Icon -->
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
    </div>
    <div class = "about_container">
        <div class="intro">
            <div class="content">
                <h2> Hello,</h2>
                <h2>I'm Nishit Nagpal </h2>
                <p>
                    I am a Data Scientist, Data Analyst, and Web Developer passionate about leveraging data-driven insights to solve complex problems while creating seamless, user-centered digital experiences. 
                    <br /><br />
                    My expertise spans across data processing, statistical analysis, machine learning, and predictive modeling, enabling me to translate raw data into actionable insights.
                    Skilled in front-end technologies, I build user-friendly applications that reflect both functionality and aesthetic appeal.
                    This combination of data expertise and development skills enables me to approach projects from both a technical and a design perspective, ensuring solutions are as impactful as they are user-centered.
                </p>
            </div> 
            <img src="./images/file.png" alt="Pofile Image">
        </div>
        <div class=" skills">
            <h3> Skills </h3>
            <div class="carousel-container" @mouseenter="pauseAnimation" @mouseleave="resumeAnimation">
                <div class="carousel-inner" :class="{ 'paused-animation': isPaused }">
                <!-- Duplicate items for infinite scrolling -->
                    <div v-for="(imageData, index) in [...imagesData, ...imagesData]" :key="index" class="carousel-item">
                        <img :src="imageData.src" :alt="imageData.description" />
                        <p>{{ imageData.description }}</p>
                    </div>    
                </div>
            </div>
        </div>
    </div>

</template>

<style scoped>
@import '@/assets/main.css';
@import '@/components/Navbar.css';

.parent_logo-container {
    width: 100%;
    display: flex;       
    justify-content: flex-end; 
    box-sizing: border-box;
    /*align-items: center;*/
}

.about_container{
    padding: 0 2rem;
    margin: 0 auto;
    max-width: 100vw;
    width: 100%;
    box-sizing: border-box;
}

.intro{
    display: grid;
    grid-template-columns: 1fr auto;/*750px auto*/ 
    grid-column-gap: 10%; 
    margin: 3em 0 0 0;
    max-width: 100%;
    align-items: center;
}

.intro .content {
    max-width: 100%;
    text-align: justify;
}

.intro p {
    /*grid-column: 1;*/ /* Place the paragraph in the first column */
    margin-top: 2em;
    text-align: justify;
}

.intro img{
    /*grid-column: 2;*/ /* Place the image in the second column */
    justify-self: end;
    max-width: 100%; 
    height: 300px;
    display: block;
}


h3 {
    font-size: 1.4rem;
    margin: 0px;
    color: #42b883 !important;
    padding: 0px;
}

h2{
    font-size: 1.8rem;
    margin-top: 1em;
    color: #42b883 !important;
    margin-bottom: 0px;
}


.skills {
    display: inline-block;
    /*padding-top: 18em;*/
    
    /*position: relative;*/
    
    height: auto;
    margin: 1em 1em 1em 0em;
    width: 100%;
}

.carousel-container {
  overflow: hidden;
  position: relative;
  width: 100%;
  height: 200px; /* Adjust as needed */
}

.carousel-inner {
  display: flex;
  width: max-content;
  animation: scroll 30s linear infinite;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  gap: 30px;
}

.carousel-item {
  flex: 0 0 auto;  
  width: 120px; /* Adjust as needed */
  text-align: center;
  border: 2px solid #42b883;
  padding: 1em 0px 0px 0px;
  margin-top: 1em;
  box-shadow: 0 0 10px 5px transparent;
}

.carousel-item img {
  width: 50px; /* Adjust as needed */
  height: auto;
}

.carousel-inner.paused-animation {
  animation-play-state: paused;
}

@keyframes scroll {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-50%);
  }
}
@media (hover: hover) {
    .carousel-item:hover {
        cursor: pointer;
        box-shadow: 0 0 10px 5px #42b883;
    }

    .carousel-item:hover {
        transform: scale(1.15);
        cursor: pointer;
    }
}
button:active{
    transform: translateY(2px);
}

.paused-animation {
    animation-play-state: paused; 
}


/*
@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
*/
   
.font-change .intro p{
    font-size: 20px;
    margin-bottom: 0px;
    margin-top: 10px;
}

.font-change .image-item{
    margin-top: 10px;
}


/* Hamburger Menu */

.hamburger-container {
  display: none; /* Hide hamburger menu on larger screens */
  position: fixed;
  margin-top: 0;
  margin-right: 2rem;
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


/* Responsive Grid for Smaller Screens */
@media screen and (max-width: 768px) {
    .hamburger-container {
        display: block; /* Show hamburger menu on smaller screens */
    }
    .navbar.isHamburgerMenuOpen nav {
        display: block;
    }
}

@media screen and (max-width: 478px) {

    .intro {
        display: flex;
        flex-direction: column; /* Stack items vertically */
        align-items: center; /* Center items horizontally */
        gap: 1rem; /* Add space between elements */
    }

    .intro img {
        max-width: 100%; /* Ensure the image scales within the container */
        height: auto; /* Maintain aspect ratio */
        margin-bottom: 1rem; /* Add space below the image */
        height: 200px;
        width: auto;
    }
    .intro h2{
        text-align: left;
    }
}

</style>