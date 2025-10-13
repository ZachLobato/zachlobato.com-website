<template>
  <div class="lg:grid lg:grid-cols-12">
    <header class="h-screen flex flex-col justify-around lg:justify-between lg:mt-20 lg:fixed lg:right-1/2 lg:w-1/3">
      <div v-if="!isLargeScreen"></div>
      <div class="flex flex-col justify-center">
        <h1 class="text-5xl text-center lg:text-left dark:text-pistachio-200 text-pistachio-800 mb-4 lg:mb-6">Zach Lobato</h1>
        <h2 class="text-xl text-center lg:text-left dark:text-pistachio-200 text-pistachio-800 mb-20 lg:mb-6">Husband, Father, Software Engineer</h2>
        <p class="text-lg dark:text-cadet-gray-200 text-cadet-gray-800 text-base text-center lg:text-left">I make products customers love.</p>
      </div>
      <ul v-if="isLargeScreen" class="dark:text-cadet-gray-200 text-cadet-gray-800 flex flex-col gap-5">
        <li :class="{
          'ml-2': mostVisible === 'products',
          'transition-all': true,
        }">
          <a :class="{ 
            'dark:text-prussian-blue-200': true,
            'text-prussian-blue-800': true,
            'dark:text-mint-green-200': mostVisible === 'products',
            'dark:hover:text-mint-green-200': true,
            'hover:text-mint-green-800': true,
            'relative': true,
            'flex items-center': true,
          }" href="#products">        
          <div :class="{
            'absolute': true,
            'left-0': true,
            'top-0': true,
            'bottom-0': true,
            'p-0': true,
            'm-0': true,
            'hidden': mostVisible !== 'products',
            'w-1': mostVisible === 'products',
            'bg-cadet-gray-400': true,
          }"></div>
          <div :class="{
            'ml-4': mostVisible === 'products',
            'transition-all': true,
          }">Products</div>
          </a>
        </li>

        <li :class="{
          'ml-2': mostVisible === 'philosophy',
          'transition-all': true,
        }">
          <a :class="{ 
            'dark:text-prussian-blue-200': true,
            'text-prussian-blue-800': true,
            'dark:text-mint-green-200': mostVisible === 'philosophy',
            'dark:hover:text-mint-green-200': true,
            'hover:text-mint-green-800': true,
            'relative': true,
            'flex items-center': true,
          }" href="#philosophy">        
          <div :class="{
            'absolute': true,
            'left-0': true,
            'top-0': true,
            'bottom-0': true,
            'p-0': true,
            'm-0': true,
            'hidden': mostVisible !== 'philosophy',
            'w-1': mostVisible === 'philosophy',
            'bg-cadet-gray-400': true,
          }"></div>
          <div :class="{
            'ml-4': mostVisible === 'philosophy',
            'transition-all': true,
          }">Philosophy</div>
          </a>
        </li>

        <li :class="{
          'ml-2': mostVisible === 'experience',
          'transition-all': true,
        }">
          <a :class="{ 
            'dark:text-prussian-blue-200': true,
            'text-prussian-blue-800': true,
            'dark:text-mint-green-200': mostVisible === 'experience',
            'dark:hover:text-mint-green-200': true,
            'hover:text-mint-green-800': true,
            'relative': true,
            'flex items-center': true,
          }" href="#experience">        
          <div :class="{
            'absolute': true,
            'left-0': true,
            'top-0': true,
            'bottom-0': true,
            'p-0': true,
            'm-0': true,
            'hidden': mostVisible !== 'experience',
            'w-1': mostVisible === 'experience',
            'bg-cadet-gray-400': true,
          }"></div>
          <div :class="{
            'ml-4': mostVisible === 'experience',
            'transition-all': true,
          }">Experience</div>
          </a>
        </li>
      </ul>
      <ul class="flex flex-row space-x-8 justify-center lg:justify-start lg:content-end lg:mb-40">
        <li><a target="_blank" href="https://bsky.app/profile/zachlobato.com" class="dark:text-prussian-blue-200 text-prussian-blue-800 hover:text-mint-green-800 dark:hover:text-mint-green-200" aria-label="Personal BlueSky Link" alt="Personal BlueSky Link" title="Personal BlueSky Link" rel="noopener noreferrer"><IconBlueSky></IconBlueSky></a></li>
        <li><a target="_blank" href="https://github.com/ZachLobato" class="dark:text-prussian-blue-200 text-prussian-blue-800 hover:text-mint-green-800 dark:hover:text-mint-green-200" aria-label="Personal GitHub Link" alt="Personal GitHub Link" title="Personal GitHub Link" rel="noopener noreferrer"><IconGithub></IconGithub></a></li>
        <li><a target="_blank" href="https://www.instagram.com/zachlobato" class="dark:text-prussian-blue-200 text-prussian-blue-800 hover:text-mint-green-800 dark:hover:text-mint-green-200" aria-label="Personal Instagram Link" alt="Personal Instagram Link" title="Personal Instagram Link" rel="noopener noreferrer"><IconInstagram></IconInstagram></a></li>
        <li><a target="_blank" href="https://www.linkedin.com/in/zachlobato" class="dark:text-prussian-blue-200 text-prussian-blue-800 hover:text-mint-green-800 dark:hover:text-mint-green-200" aria-label="Personal LinkedIn Link" alt="Personal LinkedIn Link" title="Personal LinkedIn Link" rel="noopener noreferrer"><IconLinkedIn></IconLinkedIn></a></li>
      </ul>
    </header>
    <main class="lg:col-start-7 lg:col-span-5 lg:mr-6" id="main">
      <div class="flex" id="products">
        <div class="block m-auto min-h-screen w-full">
          <h2 v-show="!isLargeScreen"
            :class="{
              'bg-cadet-gray-200/20': true,
              'dark:bg-cadet-gray-800/20': true,
              'dark:text-pistachio-200': true,
              'flex-col': true,
              'flex': true,
              'grid-row': true,
              'h-16': true,
              'justify-center': true,
              'mx-0': true,
              'px-4': true,
              'sticky': true,
              'text-3xl': true,
              'text-pistachio-800': true,
              'top-0': true,
              'z-10': true,
              'backdrop-blur-sm': true,
            }"
          >
            Products
          </h2>
          <h3 class="flex flex-col justify-center grid-row text-lg text-pistachio-800 dark:text-pistachio-200  mt-6 lg:mt-20 mb-6 mx-4 lg:mx-0 lg:px-0 lg:text-2xl">Latest Updated</h3>
          <div class="flex justify-center lg:justify-normal gap-4 flex-wrap mx-4 drop-shadow-[0_4px_8px_rgba(255,255,255,0.25)] dark:drop-shadow-[0_4px_8px_rgba(0,0,0,0.75)]">
            <div v-if="data.isLoading">Loading...</div>
            <MaterialCard v-else v-for="(card, index) in data.info" :key="index"
              :banner-video-url="card.banner_video_url"
              :banner-dark-video-url="card.banner_dark_video_url"
              :launch-url="card.launch_url"
              :github-url="card.github_url"
              :notion-url="card.notion_url"
              :under-construction="card.under_construction"
              :title="card.title"
              :updated-at="card.updated_at"
              :isWebPageMirror="card.isWebPageMirror"
              :mirrorMaxDepth="card.mirrorMaxDepth"
              :sub-title="card.sub_title"></MaterialCard>
          </div>
        </div>
      </div>
      <div class="flex w-full" id="philosophy">
        <div class="block m-auto min-h-screen w-full">
          <h2 v-show="!isLargeScreen" class="sticky top-0 flex flex-col px-4 justify-center grid-row text-3xl text-pistachio-800 dark:text-pistachio-200 h-16 w-full bg-cadet-gray-200/20 dark:bg-cadet-gray-800/20 backdrop-blur-sm mx-0">
            Philosophy
          </h2>
          <h3 class="flex flex-col px-4 justify-center grid-row text-lg text-pistachio-800 dark:text-pistachio-200  mt-6 lg:mt-20 mb-6 mx-0 lg:px-0 lg:text-2xl">A Product Approach</h3>
          <article class="mt-4 mx-4 dark:text-cadet-gray-200 text-cadet-gray-800 text-base text-left mb-4">
            <p>When it comes to making products, there's always a race against time. The school of product with which I subscribe to (inspired by <a target="_blank" class="dark:text-prussian-blue-200 text-prussian-blue-800 hover:text-mint-green-800 dark:hover:text-mint-green-200" href="https://jpattonassociates.com/">Jeff Patton</a>) optimizes what precious time we have by defining clear boundaries of responsibility while simultaneously encouraging asynchronous collaboration.</p>
            <br />
            <h4 class="text-pistachio-600 dark:text-pistachio-400 uppercase font-bold text-base">Opportunity Discovery</h4>
            <p>Product Managers identify opportunities or problems to solve by understanding their customers. They shorten the feedback loop with their customers and steer the overall strategy for the product team.</p>
            <br />
            <ul class="list-disc list-inside mx-4">
              <li>Understanding every feature and service offered by the their product</li>
              <li>As fixes and features are delivered, tracking user satisfaction and target customer willingness to join.</li>
              <li>Using feedback for making next decisions on the product.</li>
            </ul>
            <br />
            <h4 class="text-pistachio-600 dark:text-pistachio-400 uppercase font-bold text-base">Solution Discovery</h4>
            <p>Taking the next highest priority opportunity, Product Designers drive the effort to come up with the next best solution.</p>
            <br />
            <ul class="list-disc list-inside mx-4">
              <li>Using their expertise to design experiences to try with our customers.</li>
              <li>Confirming their design is feasible and addresses the problem or opportunity.</li>
              <li>Confirming usability with customer feedback</li>
            </ul>
            <br />
            <h4 class="text-pistachio-600 dark:text-pistachio-400 uppercase font-bold text-base">Solution Marketing</h4>
            <p>Product Marketing now takes action in determining how best to communicate this upcoming solution.</p>
            <br />
            <ul class="list-disc list-inside mx-4">
              <li>Evaluate how to market the solution</li>
              <li>Facilitate communication to internal stakeholders</li>
              <li>Facilitate communication to external stakeholders</li>
            </ul>
            <br />
            <h4 class="text-pistachio-600 dark:text-pistachio-400 uppercase font-bold text-base">Solution Delivery</h4>
            <p>The design is complete and it's time to deliver.</p>
            <br />
            <ul class="list-disc list-inside mx-4">
              <li>Architect the right solution for the feature.</li>
              <li>Deliver on that architecture.</li>
            </ul>
          </article>
        </div>
      </div>
      <div class="flex w-full" id="experience">
        <div class="block m-auto min-h-screen w-full">
          <h2 v-show="!isLargeScreen" class="sticky top-0 flex flex-col px-4 justify-center grid-row text-3xl text-pistachio-800 dark:text-pistachio-200 h-16 w-full bg-cadet-gray-200/20 dark:bg-cadet-gray-800/20 backdrop-blur-sm mx-0">
            Experience
          </h2>
          <div class="flex flex-row mx-4 lg:mx-0 mt-6 mb-6 lg:mt-20 lg:px-0 text-pistachio-800 dark:text-pistachio-200 justify-between">
            <h3 class="flex flex-col justify-center grid-row text-lg mx-0 lg:text-2xl">UHIN</h3>
            <div>03/2017 to Present</div>
          </div>
          <div class="mx-4 mb-2">
            <h4 class="text-pistachio-600 dark:text-pistachio-400 uppercase font-bold text-base">Principal Software Engineer</h4>
            <h5 class="text-cadet-gray-800 dark:text-cadet-gray-200 font-bold text-xs">{{ latestPositionDuration }}</h5>
          </div>
          <p class="mx-4 mb-4 text-cadet-gray-800 dark:text-cadet-gray-200">Manage and train multiple software engineers while working very closely with a Product Manager and Product Designer on a core product team. Coordinate team’s efforts with company’s larger security and compliance goals.</p>
          <div class="mx-4 mb-2">
            <h4 class="text-pistachio-600 dark:text-pistachio-400 uppercase font-bold text-base">Senior Software Engineer</h4>
            <h5 class="text-cadet-gray-800 dark:text-cadet-gray-200 font-bold text-xs">1 Year 11 Months</h5>
          </div>
          <p class="mx-4 mb-4 text-cadet-gray-800 dark:text-cadet-gray-200">Replaced legacy claim submission software with a more intuitive and collaborative web application. Lowered claim submission times from tens of minutes to seconds with “templates” implementation.</p>
          <div class="mx-4 mb-2">
            <h4 class="text-pistachio-600 dark:text-pistachio-400 uppercase font-bold text-base">Software Engineer</h4>
            <h5 class="text-cadet-gray-800 dark:text-cadet-gray-200 font-bold text-xs">2 Years 8 Months</h5>
          </div>
          <p class="mx-4 mb-4 text-cadet-gray-800 dark:text-cadet-gray-200">Understood and maintained legacy Healthcare EDI protocols. Started a chain of events that eventually has led to the future replacement of the entire Clearinghouse.</p>
          <div class="flex flex-row mx-4 lg:mx-0 mt-6 mb-6 lg:px-0 text-pistachio-800 dark:text-pistachio-200 justify-between">
            <h3 class="flex flex-col justify-center grid-row text-lg mx-0 lg:text-2xl">Navitaire</h3>
            <div>07/2016 to 03/2017</div>
          </div>
          <div class="mx-4 mb-2">
            <h4 class="text-pistachio-600 dark:text-pistachio-400 uppercase font-bold text-base">Software Developer</h4>
            <h5 class="text-cadet-gray-800 dark:text-cadet-gray-200 font-bold text-xs">9 Months</h5>
          </div>
          <p class="mx-4 mb-4 text-cadet-gray-800 dark:text-cadet-gray-200">Maintained and updated .NET code (C#, MSMQ, and SQL) while collaborating with an international team on large scale code changes. Created documentation and trainings for tools and software that previously did not exist, to hopefully decrease training time for new employees.</p>
          <div class="flex flex-row mx-4 lg:mx-0 mt-6 mb-6 lg:px-0 text-pistachio-800 dark:text-pistachio-200 justify-between">
            <h3 class="flex flex-col justify-center grid-row text-lg mx-0 lg:text-2xl">University of Utah</h3>
            <div>05/2015 to 08/2015</div>
          </div>
          <div class="mx-4 mb-2">
            <h4 class="text-pistachio-600 dark:text-pistachio-400 uppercase font-bold text-base">Teaching Assistant</h4>
            <h5 class="text-cadet-gray-800 dark:text-cadet-gray-200 font-bold text-xs">4 Months</h5>
          </div>
          <p class="mx-4 mb-4 text-cadet-gray-800 dark:text-cadet-gray-200">Maintained the responsibilities of teaching labs, holding office hours, creating assignments grading rubrics, and grading weekly assignments. Created additional course materials and held extended hours for the students’ benefit.</p>
          <!-- <div class="mt-4 text-center dark:text-cadet-gray-200 text-cadet-gray-800">
            Coming Soon.
          </div> -->
        </div>
      </div>
    </main>
  </div>
</template>


<script setup>
import MaterialCard from '../components/MaterialCard.vue'
import { onMounted, onUnmounted, reactive, ref, watchEffect, nextTick } from 'vue';
import { useRoute } from 'vue-router';
import IconBlueSky from '../components/icons/IconBlueSky.vue'
import IconGithub from '../components/icons/IconGithub.vue'
import IconInstagram from '../components/icons/IconInstagram.vue'
import IconLinkedIn from '../components/icons/IconLinkedIn.vue'

const route = useRoute();
const mostVisible = ref(''); // This ref will store the ID of the most visible element
const latestPositionDuration = ref('');

function calculateDifference() {
  const date = new Date('2021-08-01');
  const now = new Date();

  let years = now.getFullYear() - date.getFullYear();
  let months = now.getMonth() - date.getMonth();

  if (months < 0) {
    years -= 1;
    months += 12;
  }

  return formatDifference(years, months);
}

function formatDifference(years, months) {
  const yearStr = years === 1 ? '1 Year' : `${years} Years`;
  const monthStr = months === 1 ? '1 Month' : `${months} Months`;
  
  if (years === 0) {
    return monthStr;
  } else if (months === 0) {
    return yearStr;
  } else {
    return `${yearStr} ${monthStr}`;
  }
}

function handleIntersect(entries, observer) {
  let maxVisibility = 0;
  let mostVisibleId = '';

  entries.forEach((entry) => {
    const currentVisibility = entry.intersectionRatio; // How much of the element is visible
    if (currentVisibility > maxVisibility) {
      maxVisibility = currentVisibility;
      mostVisibleId = entry.target.id; // Update the most visible element's ID
    }
  });

  mostVisible.value = mostVisibleId; // Update the reactive reference
}

let observer;

function detectMostVisible() {
  const options = {
    root: null,
    rootMargin: '0px',
    threshold: [0.55] // Adjust as necessary to tweak when changes occur
  };

  observer = new IntersectionObserver(handleIntersect, options);

  // Add all elements you to be observedß
  ['products', 'philosophy', 'experience'].forEach(id => {
    const element = document.getElementById(id);
    if (element) {
      observer.observe(element);
    }
  });
}

onUnmounted(() => {
  if (observer) {
    observer.disconnect();
  }
}); 



function scrollToElementById(elementId) {
  const element = document.getElementById(elementId);
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' });
  }
}

watchEffect(() => {
  const hash = route.hash;
  const showProducts = hash.includes('#products');
  const showExperience = hash.includes('#experience');

  if (showProducts) {
    nextTick(() => {
      scrollToElementById('products');
    });
  } else if (showExperience) {
    nextTick(() => {
      scrollToElementById('experience');
    });
  }
});

// Define reactive state to store API data and loading state
const data = reactive({
  info: null,
  isLoading: true,
});

const isLargeScreen = ref(false);

function checkScreenSize() {
  const query = window.matchMedia('(min-width: 1024px)');
  isLargeScreen.value = query.matches;
  query.addEventListener('change', (e) => {
    isLargeScreen.value = e.matches;
  });

  // Clean-up function to remove event listener when component unmounts
  onUnmounted(() => {
    query.removeEventListener('change', (e) => {
      isLargeScreen.value = e.matches;
    });
  });
}

// Function to fetch data from an API
const fetchData = async () => {

  try {
    // todo: connect to real api
    // const response = await fetch('https://api.example.com/data');
    // const jsonData = await response.json();
    data.info = [
      {
        launch_url: "https://zachlobato.com",
        github_url: "https://github.com/ZachLobato/zachlobato.com-website",
        notion_url: "https://riticulous.notion.site/Zach_Lobato_Website_a1e47722d50a44688f6ff9211d7d25cb",
        title: "Personal Website",
        sub_title: "For the latest on me",
        updated_at: "2025-10-13",
        isWebPageMirror: true,
        mirrorMaxDepth: 3,
      },
      {
        banner_video_url: 'https://i.imgur.com/N1tahcD.mp4',
        banner_dark_video_url: 'https://i.imgur.com/N1tahcD.mp4',
        under_construction: true,
        title: 'Oracle: A Lab Time Ago',
        sub_title: 'A time and space adventure',
        updated_at: "2024-02-18",
        isWebPageMirror: false,
      },
    ]
  } catch (error) {
    console.error("Failed to fetch data:", error);
  } finally {
    data.isLoading = false; // Update loading state
  }
};

onMounted(() => {
  fetchData();
  checkScreenSize();
  detectMostVisible();
  latestPositionDuration.value = calculateDifference();

  nextTick(() => {
    const hash = window.location.hash;
    const showProducts = hash.includes('#products');
    const showExperience = hash.includes('#experience');
    if (showProducts) {
      scrollToElementById('products');
    } else if (showExperience) {
      scrollToElementById('experience');
    }
  });
});

</script>