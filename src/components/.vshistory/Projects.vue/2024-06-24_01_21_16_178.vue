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
//import portfoliodesktopImage from '@/components/images/portfolio-desktop.png';

export default {
  data() {
    return {
      projects: [
        {
        id: 1,
        image: resumedesktopImage,
        title: 'Resume Website Built with React.js.' ,
        description: 'React.js along with HTML and CSS modifications to create a dynamic, responsive and visually appealing digital representation of my resume designed to showcase my experience, skills, and educational background.',
        liveLocation: 'https://nishitnagpal.github.io/cv',
        buttons: ['JavaScript', 'React'],
        githubLink: 'https://github.com/nishitnagpal/cv'
        },
        {
        id: 2,
        image: shoppingdesktopImage,
        title: 'Real-Life Shopping Cart Application with React, TypeScript, and Vite',
        description: 'User-friendly shopping cart application with intuitive interface allows users to browse through a wide range of products, and add them to their cart.',
        liveLocation: 'https://nishitnagpal.github.io/shoppingcart/',
        buttons: ['TypeScript', 'React','Vite', 'SASS'],
        githubLink: 'https://github.com/nishitnagpal/shoppingcart'
        },
        {
        id: 3,
        image: websitedesktopImage,
        title: 'Learning Ability and Adaptivity of Digital Consulting Assistant and Content Management System' ,
        description: 'WordPress-based knowledge base to aid elderly, disabled, and vulnerable individuals with chatbot and other plugins to teach the site to learn and adapt to user interactions. ',
        liveLocation: 'https://nishitnagpal.github.io/thesiswebsite',
        buttons: ['WordPress', 'mySQL', 'PHP', 'NLP'],
        githubLink: 'https://github.com/nishitnagpal/thesiswebsite'
        }
        /*
        {
        id: 4,
        image: webflowdesktopImage,
        title: 'Collection of arcade style games written in Python and assembled in Webflow' ,
        description: 'These games, originally written in Pygame, have been deployed via GitHub Pages after converting the Python files to JavaScript. All the games are then compiled in Webflow, which offers a user-friendly platform for website design. ',
        liveLocation: 'https://retro-style-python-games.webflow.io/',
        buttons: ['Webflow', 'Pygame', 'JavaScript', 'HTML5'],
        githubLink: 'https://github.com/nishitnagpal/webflowpygame'
        }*/
      ]
    };
  },
}
</script>

<template>
    <div class="projects">
        <div v-for="project in projects" :key="project.id" class="project-item">
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
</template> 

<style scoped>

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
}

.project-item:hover{
    transition: background-color 0.3s, color 0.3s;
    box-shadow: 0 0 10px 5px #42b883;
}

.project-image {
    width: 350px;
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
}

.button {
    background-color: transparent;
    color: white;
    border: 2px solid #42b883;
    padding: 0.375rem 0.75rem;
    border-radius: 5rem;
    margin: 0  0 5px 10px;
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
 

.contrast .button {
    color: black;
}

.font-change p{
    font-size: 20px;
}

</style>



