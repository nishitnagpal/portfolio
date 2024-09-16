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
    import catiaImage from '@/components/images/catia.png';
    import solidworksImage from '@/components/images/solidworks.svg';
    import unityImage from '@/components/images/unity.svg';
    import jiraImage from '@/components/images/jira.svg';

export default {
  data() {
     return {
        imagesData: [
            {
                src: autocadImage,
                description: 'AutoCAD'
            },
            {
                src: catiaImage,
                description: 'CATIA'
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
                src: mysqlImage,
                description: 'mySQL'
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
                 src: pythonImage,
                 description: 'Python'
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
                 src: matlabImage,
                 description: 'MATLAB'
             }
        ],
        enlarge: false,
        showEducation: false,
        showExperience : false,
        expandableVisible: reactive ({
            education_section1: false,
            education_section2: false,
            experience: false
        })
     };
  },
  mounted() {
        this.createImageElements();
        this.pauseAnimation();
        this.resumeAnimation();

        this.$el.addEventListener('click', this.handleClickOutside);
  },
  beforeUnmount() {
        this.$el.removeEventListener('click', this.handleClickOutside);
  },
  methods: {
        handleClickOutside(event) {
            // Check if the click event target is outside of the sections
            const educationSection = document.getElementById('education');
            const experienceSection = document.getElementById('experience');
        
            if (!experienceSection.contains(event.target) && !educationSection.contains(event.target)) {
                this.enlarge = false; // Return sections to normal size
            }
        },
        createImageElements() {
           const container = document.querySelectorAll(".scroller");

           container.forEach(container => {
                this.imagesData.forEach(imageData => {
                    const imageItem = document.createElement('div');
                    imageItem.classList.add('image-item');

                    const image = document.createElement('img');
                    image.src = imageData.src;

                    const description = document.createElement('p');
                    description.textContent = imageData.description;

                    imageItem.appendChild(image);
                    imageItem.appendChild(description);
                    container.appendChild(imageItem);
                });
           });
        },
        pauseAnimation() {
            const containers = document.querySelectorAll(".scroller-inner");
            containers.forEach(container => {
                container.classList.add('paused-animation')
            });
        },
        resumeAnimation() {
            const containers = document.querySelectorAll(".scroller-inner");
            containers.forEach(container => {
                container.classList.remove('paused-animation')
            });
        },
        
        toggleEnlarge(sectionId, event) {
            // Check if the click event target is the "Show More" or "Show Less" button
            if (!event.target.classList.contains('show-more') && !event.target.classList.contains('show-less')) {
                // If not, toggle the enlargement status of the section
                if (this.enlarge === sectionId) {
                    this.enlarge = false;
                } else {
                    this.enlarge = sectionId;
                }
            }
        },
        
        scrollToAnchor(sectionId) {
            const element = document.getElementById(sectionId);
            if (element) {
                element.scrollIntoView({ behavior: 'smooth' });
                this.enlarge = sectionId; // Enlarge the scrolled-to section
            }
        },
        toggleExpand(sectionId) {
            // Toggle expandable content for the given section
            /*
            const expandableContent = document.getElementById(sectionId).querySelector('.expandable');
            const showMoreButton = expandableContent.querySelector('.show-more');

            expandableContent.classList.toggle('visible');

            if (expandableContent.classList.contains('visible')) {
                showMoreButton.textContent = 'Show Less';
            } else {
                showMoreButton.textContent = 'Show More';
            }*/
            //this.expandableVisible = !this.expandableVisible;
           
           this.expandableVisible[sectionId] = !this.expandableVisible[sectionId] ;
        }
  }
}   
</script>

<template>
    <div class="intro">
        <div class="content">
            <h2> Hello, I'm Nishit Nagpal </h2>
            <p>
                As an enthusiastic frontend web developer, I love to weave together code and creativity,
                crafting responsive websites that not only function seamlessly across browsers but also captivate and delight users.
                With a keen eye for detail and a thirst for innovation, I strive to create memorable digital experiences.
                Let's embark on this exciting journey together and bring ideas to life!
            </p>
            
            <button class="scroll-button" @click="scrollToAnchor('education')">  Education </button>
            <button class="scroll-button" @click="scrollToAnchor('experience')"> Experience </button>
        </div> 
        <img src="./images/file.png" alt="Pofile Image">
    </div>
    <div class=" skills">
        <h3> Skills </h3>
        <div class="image-container" @mouseenter="pauseAnimation" @mouseleave="resumeAnimation">
            <div class="scroller-inner">

                <div v-for="(imageData, index) in imagesData" :key="index" class="image-item">
                    <div class="image-box">

                        <img :src="imageData.src" :alt="imageData.description" class="image" />
                        <p>{{ imageData.description }}</p>

                    </div>
                </div>
            </div>
        </div>
    </div>
    <div class="sections">
        <div class="education" @click="toggleEnlarge('education', $event)" :class="{ 'enlarged': enlarge === 'education', 'faded-out': enlarge === 'experience' }">
            <!-- Content of the education div goes here -->
            <h3 id="education"> Education </h3>
            <p>
                <span class="visible">
                    Master of Science in Mechatronics, <br /> University of Siegen, Germany <br /> Oct 2018 - Dec 2022 <br /> <br />
                    <span class="show_more" @click="toggleExpand('education_section1'), toggleEnlarge('education', $event)"> Thesis: A study on the Learning Ability and Adaptivity of the Digital Consulting Assistant and Content Management System of LOKAL-Digital Project <br /> </span>
                </span>
                <span :class="{ 'visible': expandableVisible['education_section1'], 'hidden': !expandableVisible['education_section1'] }">
                    A knowledge base aimed at assisting elderly, disabled and vulnerable group was built using WordPress as Content Management System for the city of Netphen in collaboration with the University of Siegen. Resources in form of advertisements and listings throught this knowledge bank were made available in the fields of housing facility providers, caregivers, nursing homes, and other healthcare facilities.
                    <br />
                    Thesis investigates ways in which plugins can be used to train the website to learn and adapt to user interactions. A plugin for managing taxonomies was installed that can auto-suggest terms after indexing content, making it easier to categorize posts on basis of different categories and tags. A chatbot integrated with the Natural Language Understanding platform was added to the website to interact with users, understand their intent, and guide them to relevant content on the website.
                    <br />
                   <!-- <span class="show_less" @click="toggleExpand('education'), toggleEnlarge('education', $event)"> Show Less </span> -->
                </span>
            </p>
            <p>
                <span class="visible">
                    Bachelor of Technology in Mechanical Engineering, <br />Institute of Engineering &amp; Management, Kolkata, India <br /> Sep 2013 - Jun 2017 <br /> <br />
                    <span class="show_more" @click="toggleExpand('education_section2'), toggleEnlarge('education', $event)"> Project: Performance Measurement Of Green Supply Chains In The Indian Manufacturing Sector Using The Analytical Network Process  <br /></span>
                </span>
                <span :class="{ 'visible': expandableVisible['education_section2'], 'hidden': !expandableVisible['education_section2'] }">
                    Developed a performance measurement system for a green supply chain using a green balanced scorecard and Analytical Network Process (ANP) with companies in Indian manufacturing sector as case study.
                    This study modified the balanced scorecard by adding a fifth environmental perspective under which green activities were listed as performance metrics. The critical success factors
                    of the green supply chain management (GSCM) were studied to understand the performance metrics of the balanced scorecard perspectives and develop the ANP network model. The model was used to find how green the companies in case study were considering the different sustainable constructs. Further scope inlcuded expanding model framework
                    to provide the key constructs or area upon which the manufacturing sector in India needs to work to make the system green.
                    <br />
                   <!-- <span class="show_less" @click="toggleExpand('education'), toggleEnlarge('education', $event)"> Show Less </span> -->
                </span>
            </p>
        </div>
        <div class="experience" @click="toggleEnlarge('experience', $event)" :class="{ 'enlarged': enlarge === 'experience', 'faded-out': enlarge === 'education' }">
            <!-- Content of the experience div goes here -->
            <h3 id = "experience"> Experience </h3>
            <p>
                <span class="visible">
                    Flink GmbH <br /> Software Engineer, Aug. 2023 - April 2024 <br /> <br />
                    - Revamped the warehouse management system's user interface to clearly detail FIFO processes for each article, reducing restocking time by 50%.  <br />
                    - Redesigned the desktop website to include a click-and-collect ordering option, enhancing the user experience and significant increase in online orders by 25%. <br />
                    <span @click="toggleEnlarge('experience', $event)"> <br /> </span>
                </span>
            </p>
            <p>
                <span class="visible">
                    Sterling & Wilson Pvt. Ltd. <br /> Engineer-Planning, July 2017- Sept. 2018 <br /> <br />
                    - Undertook crucial responsibilities in quality inspection and control visits. <br />
                    - Played a pivotal role in devising and executing strategies geared towards cost reduction and optimal resource utilization. <br />
                    - Prepared contracts, encompassing both sales and technical aspects, for ventures centered on the engineering, planning, installation, and maintenance of HVAC systems. <br /> <br />
                    <span  class="show_more" @click="toggleExpand('experience'), toggleEnlarge('experience', $event)"> Noteworthy projects included collaborations with esteemed entities: <br /> </span>
                </span>
                <span :class="{ 'visible': expandableVisible['experience'], 'hidden': !expandableVisible['experience'] }">
                    <ul>
                        <li> Kolkata Metro Rail Corporation, a distinguished Government of India enterprise wholly owned and funded by the Ministry of Railways. </li>
                        <li> National Thermal Power Corporation (NTPC), a prominent Indian central Public Sector Undertaking under the aegis of the Ministry of Power, particularly at their plant in Rourkela, Orissa, India. </li>
                        <li> NSPCL, a joint venture between NTPC and SAIL (Steel Authority of India Limited), a key player in the Indian central Public Sector Undertaking domain, with a focus on the plant situated in Bhilai, Chhattisgarh, India. </li>
                        <li> ABB's groundbreaking Raigarh-Pugalur 800kV ultra-high-voltage direct current (UHVDC) system, facilitating vital connectivity between central and South India. </li>
                    </ul>
                    <br />
                    <!-- <span class="show_less" @click="toggleExpand('experience'), toggleEnlarge('experience', $event)"> Show Less </span> -->
                </span>
            </p>
        </div>
    </div>

</template>

<style scoped>

.sections{
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 10%;
}

.intro{
    display: grid;
    grid-template-columns: 750px auto; 
    grid-column-gap: 10%; 
    margin: 3em 0 0 0;
}

.intro p {
    grid-column: 1; /* Place the paragraph in the first column */
    margin-top: 2em;
}

.intro img{
    grid-column: 2; /* Place the image in the second column */
    max-width: 100%; /* Ensure the image stays within its container */
    height: 300px;
    width: auto;
}
h3 {
    font-size: 1.4rem;
    margin-top: 0px;
    color: #42b883 !important;
    margin-bottom: 0px;
}

h2{
    font-size: 1.8rem;
    margin-top: 1em;
    color: #42b883 !important;
    margin-bottom: 0px;
}

button {
    background-color: #42b883;
    color: black;
    border: 1px solid #42b883;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: 10px;
    transition: transform 0.3s ease-in-out;
    margin: 1em 2em 1em 0em;
    cursor: pointer;
}

.skills {
    display: inline-block;
    /*padding-top: 18em;*/
    position: relative;
    height: auto;
    margin: 1em 1em 1em 0em;
    width: 100%;
}

.image-container {
    display: flex;
    overflow-x: hidden;
    width: 100%;
}

.image-box {
    display: flex;
    flex-direction: column;
    align-items: center;
    border: 2px solid #42b883;
    padding: 1em 0px 0px 0px;
    width: 130px;
    height: auto;
    box-shadow: 0 0 10px 5px transparent;
}

.image-item {
    
    margin: 2em 2em 2em 2em;
    
}
.image-item img {
    height: auto;
    width: 50px;
    border-radius: 0px;
}

.image-item p {
    margin-top: 15px;
    font-size: 18px;
    text-align: center;
}

/*.scroller
.image-container{
    width: 600px;
    overflow: hidden;
}
*/

.scroller-inner{
    display: flex;
    width: max-content;
    flex-wrap: nowrap;
    animation: scroll 30s linear infinite;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}
/*
.scroller-inner img{
    width: 50px;
    height: auto;
}
 */

@keyframes scroll{
    to{
        transform: translate(-50%);
    }
}
 
/*
 @keyframes scroll {
    0% {
        transform: translateX(0%);
    }

    100% {
        transform: translateX(-100%);
    }
}
*/

@media (hover: hover) {
    .image-box:hover {
        cursor: pointer;
        box-shadow: 0 0 10px 5px #42b883;
    }

    .image-item:hover {
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

    /* Add transition for opacity */
    .education, .experience {
        transition: opacity 0.3s ease-in-out;
    }

    /* Define styles for enlarged section */
    .education.enlarged, .experience.enlarged {
        transform: scale(1.2);  
    }

    .education.enlarged {
       box-shadow: 0 0 5px 5px #42b883;
       margin: 2em 0em 0em 4em;
       padding: 2em 0em 0em 3em;
    } 
    .experience.enlarged {
       box-shadow: 0 0 5px 5px #42b883;
       margin: 2em 4em 0em 0em;
       padding: 2em 0em 0em 3em;
    } 

    /* Define styles for faded-out section */
    .education.faded-out, .experience.faded-out {
        opacity: 0.5; /* Adjust opacity as needed */
    }
 


.Education, .Experience {
    display: none;
    max-width: 100%;
    overflow: hidden;
    transition: transform 0.3s ease-in-out;
    cursor: pointer;
    transition: opacity 0.3s ease-in-out;
}

.showEducation, .showExperience {
    display: block;
}

.Education.enlarged, .Experience.enlarged{
    transform: scale(1.2);
}

.Education.faded-out, .Experience.faded-out {
    opacity: 0.2; 
}

.visible {
  display: inline-block;
}

.hidden {
  display: none;
}

.show_more, .show_less{
    color: #42b883;
    cursor: pointer;
}

.font-change .intro p{
    font-size: 20px;
    margin-bottom: 0px;
    margin-top: 10px;
}

.font-change .image-item{
    margin-top: 10px;
}

.font-change .sections p{
    font-size: 20px;
}
</style>