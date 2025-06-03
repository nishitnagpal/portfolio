<script>
    /*
     export default {
        beforeCreate: function () {
            document.body.className = 'Projects';
        }
    }
    */
import resumedesktopImage from '@/components/images/resume-desktop.png';
import shoppingdesktopImage from '@/components/images/shopping-desktop.png';
import websitedesktopImage from '@/components/images/website-desktop.png';
import webflowdesktopImage from '@/components/images/webflow-desktop.png';
import metrodesktopImage from '@/components/images/metro-desktop.png';
import creditcardanalysisImage from '@/components/images/fraudanalysis-desktop.png';
import powerbiImage from '@/components/images/powerBI-desktop.png';
import tableauImage from '@/components/images/tableau-desktop.png';
import datascienceImage from '@/components/images/datascience.svg';
import webdevelopmentImage from '@/components/images/website.svg';

export default {
  data() {
    return {
      projects: [
        { 
        id: 1,
        category: 'data science',
        image: tableauImage,
        title: 'Interactive Sales Dashboard',
        description: 'Designed an interactive and visually appealing Tableau dashboard featuring a calendar widget filter, line chart, distribution histograms, heat map, and map visualization to analyze housing data, enabling intuitive exploration of trends and insights.',
        liveLocation: 'https://nishitnagpal.github.io/tableauProject/',
        buttons: ['Tableau', 'Data Visualisation', 'Data Insights'],
        githubLink: 'https://github.com/nishitnagpal/tableauProject'    
        },  
        {
        id: 2,
        category: 'data science',
        image: powerbiImage, 
        title: 'Dynamic Business Performance Dashboard in Power BI',
        description: 'Creation of an interactive Power BI dashboard for analyzing sales performance and customer behavior. It includes features like dynamic filtering, KPI visualizations, and region-wise sales breakdowns, highlighting actionable insights for business strategy optimization.',
        buttons: ['PowerBI', 'KPI Dashboards', 'DAX'],
        githubLink: 'https://github.com/nishitnagpal/PowerBI-project'    
        },
        {
        id: 3,
        category: 'data science',
        image: creditcardanalysisImage,
        title: 'Credit Card Fraud Analysis: A Data-Driven Approach',
        description: 'Examines fraud detection in digital payments analysing various factors and trends. Insights using ML algorithms reveal factors influencing fraud likelihood and strategies to enhance payment security.',
        liveLocation: 'https://nishitnagpal.github.io/CreditCardFraudAnalysis/report.pdf',
        buttons: ['Jupyter', 'Python', 'Data Modeling', 'ML'],
        githubLink: 'https://github.com/nishitnagpal/CreditCardFraud'    
        },
        {
        id: 4,
        category: 'web development',
        image: metrodesktopImage,
        title: 'Kolkata Metro Timings App with Next.js using Py Scrapy' ,
        description: 'A responsive Next.js app hosted through Vercel that provides real-time metro train timings using Python Scrapy to fetch and process data, ensuring users never miss their train. Features include dynamic schedules and intuitive station selection.',
        liveLocation: 'https://kolkata-metro-timings.vercel.app/',
        buttons: ['Next.js', 'Scrapy.py', 'JavaScript'],
        githubLink: 'https://github.com/nishitnagpal/KolkataMetroTimings'
        },
        {
        id: 5,
        category: 'web development',
        image: webflowdesktopImage,
        title: 'Collection of arcade style games written in Python and assembled in Webflow' ,
        description: 'These games, originally written in Pygame, have been deployed via GitHub Pages after converting the Python files to JavaScript. All the games are then compiled in Webflow, which offers a user-friendly platform for website design. ',
        liveLocation: 'https://retro-style-python-games.webflow.io/',
        buttons: ['Webflow', 'Pygame', 'JavaScript'],
        githubLink: 'https://github.com/nishitnagpal/Pygame_Webflow'
        },
        {
        id: 6,
        category: 'web development',
        image: websitedesktopImage,
        title: 'Learning Ability and Adaptivity of Digital Consulting Assistant and Content Management System' ,
        description: 'WordPress-based knowledge base to aid elderly, disabled, and vulnerable individuals with chatbot and other plugins to teach the site to learn and adapt to user interactions. ',
        liveLocation: 'https://nishitnagpal.github.io/thesiswebsite',
        buttons: ['WordPress', 'mySQL', 'PHP', 'NLP'],
        githubLink: 'https://github.com/nishitnagpal/thesiswebsite'
        },
        {
        id: 7,
        category: 'web development',
        image: shoppingdesktopImage,
        title: 'Real-Life Shopping Cart Application with React, TypeScript, and Vite',
        description: 'User-friendly shopping cart application with intuitive interface allows users to browse through a wide range of products, and add them to their cart.',
        liveLocation: 'https://nishitnagpal.github.io/shoppingcart/',
        buttons: ['TypeScript', 'React','Vite', 'SASS'],
        githubLink: 'https://github.com/nishitnagpal/shoppingcart'
        },
        {
        id: 8,
        category: 'web development',
        image: resumedesktopImage,
        title: 'Resume Website Built with React.js.' ,
        description: 'React.js along with HTML and CSS modifications to create a dynamic, responsive and visually appealing digital representation of my resume designed to showcase my experience, skills, and educational background.',
        liveLocation: 'https://nishitnagpal.github.io/cv',
        buttons: ['JavaScript', 'React'],
        githubLink: 'https://github.com/nishitnagpal/cv'
        }
      ],
      isHamburgerMenuOpen: false,
    };
  },
  computed: {
    categoryIcons() {
      return {
        'data science': datascienceImage,
        'web development': webdevelopmentImage
      };
    },
    toggleHamburgerMenu() {
      this.isHamburgerMenuOpen = !this.isHamburgerMenuOpen;
    },
  },
};
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
  <div class="projects">
    <div v-for="project in projects" :key="project.id" class="project-item">
      <div class="project-icon">
        <img v-if="categoryIcons[project.category]" :src="categoryIcons[project.category]" :alt="project.category + ' icon'" class="category-icon"/>
      </div>
      <img :src="project.image" alt="Project Image" class="project-image">
      <p class="project-description">
        <a :href="project.liveLocation" target="_blank" rel="noopener noreferrer">{{ project.description }}</a>
      </p>
        <div class="project-footer">
          <div class="github-button">
            <a :href="project.githubLink" target="_blank" rel="noopener noreferrer" class="github-link">
              <img src="./images/github.svg" alt="Github logo" class="github-icon" />
            </a>
          </div>
          <div class="project-buttons">
            <span v-for="button in project.buttons" :key="button" class="button">{{ button }}</span>
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

.projects {
  display: flex;
  width: 100%;
  justify-content: space-around; /* Items are equally spaced across the container */
  flex-wrap: wrap; /* Allows items to wrap to the next row if necessary */
  margin-top: 3em; /* Add margin to separate from the navbar */
}

.project-item {
  display: flex;
  flex-direction: column;
  margin: 0.5em;
  width: calc(33.33% - 20px);
  box-sizing: border-box;
  text-align: center;
  padding: 1em;
  border: 2px solid #42b883;
  border-radius: 20px;
  transition: transform 0.3s ease-in-out;
  /*
  position: relative;
  padding: 1em;
  */
}

.project-item:hover{
  transition: background-color 0.3s, color 0.3s;
  box-shadow: 0 0 10px 5px #42b883;
}

.project-icon {
  display: flex;
  justify-content: space-between;
  width: 30px;
  height: auto;
  /*
  position: absolute;
  top: 50px;
  left: 10px;
  width: 30px;
  height: 30px;
  */
}

.category-icon {
  width: 100%;
  height: auto;
}

.project-image {
  width: 100%; /* Ensure it scales with the container width */
  align-self: center;  
  max-width: 350px; /* Keep the maximum size for large screens */
  height: auto;
}

.project-description {
  text-align: justify;
}

.project-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto;
}

.project-buttons {     /* same as github-button */
  display: flex;
  margin-top: auto;
  align-self: flex-end;
  overflow: auto;
  align-items: center; 
}

/* Customizing the scrollbar */
.project-buttons::-webkit-scrollbar {
  width: 8px; /* Width of the scrollbar */
  height: 3px; /* Height of the horizontal scrollbar */
}

/* Styling the scrollbar track */
.project-buttons::-webkit-scrollbar-track {
  display: none;
  background: #f1f1f1; /* Light background for the track */
  border-radius: 10px; /* Rounded corners */
}

/* Styling the scrollbar thumb (the draggable part of the scrollbar) */
.project-buttons::-webkit-scrollbar-thumb {
  background: #42b883; /* Color of the scrollbar thumb */
  border-radius: 10px; /* Rounded corners */
  
}

/* Optional: Add a hover effect for the thumb */
.project-buttons::-webkit-scrollbar-thumb:hover {
  background: yellowgreen; /* Darker color when hovered */
}

.button {
  display: inline-flex;
  background-color: transparent;
  color: white;
  border: 2px solid #42b883;
  padding: 0.375rem 0.75rem;
  border-radius: 5rem;
  margin: 0  0 5px 10px;
  align-items: center;  
  justify-content: center;  
  height: auto;  
  width: auto;  
  white-space: nowrap;  
}

.github-button {
  display: flex;
}

.github-icon {
  height: 35px;
  width: auto;
}
            
a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: transform 0.3s ease-in-out;
  padding: 3px;
}
 
/* check */
.contrast-change .button {
  color: black;
}

.font-change p{
  font-size: 20px;
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


/* Media Queries for Responsiveness */

/* Tablet size */
@media (max-width: 768px) {
  .project-item {
    width: calc(50% - 20px); /* Adjust width to 50% on tablets */
  }

  .project-image {
    max-width: 300px; /* Adjust max-width on smaller screens */
  }

  .hamburger-container {
    display: block; /* Show hamburger menu on smaller screens */
  }
  .navbar.isHamburgerMenuOpen nav {
    display: block;
  }
}

/* Mobile size */
@media (max-width: 480px) {
  .project-item {
    width: calc(100% - 20px); /* Stack items vertically on mobile */
  }

  .project-image {
    max-width: 250px; /* Scale down images further for mobile */
  }

  .project-icon {
    justify-content: center; /* Center the category icon */
  }
}

</style>



