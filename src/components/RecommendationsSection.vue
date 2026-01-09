<template>
  <section class="recommendations-section">
    <h2 ref="sectionHeaderRef" class="section-title fade-in-element">Recommendations</h2>

    <a class="linkedin-card" href="https://www.linkedin.com/in/em-24/details/recommendations/?detailScreenTabIndex=0" target="_blank">
    <div ref="containerRef" class="recommendations-container fade-in-element">
      <article v-for="(recommendation, index) in displayedRecommendations" :key="index" class="recommendation-card">
        <div class="card-content">
          <img :src="recommendation.profileImage" :alt="recommendation.profileName" class="profile-image" />
          <div class="profile-info">
            <h3 class="profile-name">
                {{ recommendation.profileName }}
            </h3>
            <p class="profile-title">
              <span class="title-role">{{ recommendation.titleRole }},</span>
              <br />
              <span class="title-org" v-html="recommendation.titleOrg"></span>
            </p>
          </div>
          <p class="recommendation-text" v-html="recommendation.recommendationText">
          </p>
        </div>
      </article>
    </div>
  </a>

    <button v-if="hasMoreRecommendations" ref="showMoreBtnRef" class="more-projects-btn fade-in-element"
      @click="showAll = !showAll">
      {{ showAll ? 'Show Less' : 'Show More' }}
    </button>
  </section>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { useScrollAnimation } from '../composables/useScrollAnimation'
import GabrielaProfile from '../assets/gabriela_profile.jpeg'
import AmandaProfile from '../assets/amanda_profile.jpeg'
import YilaProfile from '../assets/yila_profile.jpeg'

interface Recommendation {
  profileImage: string
  profileName: string
  titleRole: string
  titleOrg: string
  recommendationText: string
}

const recommendations: Recommendation[] = [
  {
    profileImage: GabrielaProfile,
    profileName: 'Gabriela Cladellas',
    titleRole: 'Graphic Designer',
    titleOrg: 'World Food Programme (WFP)',
    recommendationText: `Working with Esteban was a standout experience. He quickly became a real asset through his creative thinking and ability to solve problems with non-technical audiences. He brought fresh UX/UI design, development, and coding skills to corporate, multilingual projects, turning complex ideas and data into impactful web experiences for Latin America and the Caribbean.<br/><br/>Beyond his technical skills, Esteban is collaborative and proactive, and his iterative process helped meet deadlines while testing different interactive web experiences to deliver impactful storytelling with complex data. I'd highly recommend him to any team looking for a thoughtful, motivated UX/UI designer who can lead digital projects.`,
  },
  {
    profileImage: AmandaProfile,
    profileName: 'Amanda Colon',
    titleRole: 'Residence Life Coordinator',
    titleOrg: ' Harding University',
    recommendationText: 'Esteban is great to work with. He is positive, easy to talk to and dependable. He asks questions and is always wanting to learn and grow. He has been a valued member of my team.',
  },
  {
    profileImage: YilaProfile,
    profileName: 'Yila Burgos',
    titleRole: 'Subdirector',
    titleOrg: ' Centro ¡Supérate!<br/> Fundación Alberto Motta',
    recommendationText: 'I have known Esteban since his high school years. He was a scholarship recipient at Centro ¡Supérate! Fundación Alberto Motta from 2019 to 2021. During his time at our Center, he received high-quality training in English, Computer Science, and Basic Life Skills over the course of three years.<br/><br/>Throughout his time as a ¡Supérate! scholar, Esteban demonstrated a strong commitment to his studies and excellent time management. He successfully maintained outstanding academic performance both at his high school and at our Center, while participating in various volunteering activities.',
  }

]

const sectionHeaderRef = ref<HTMLElement | null>(null)
const containerRef = ref<HTMLElement | null>(null)
const showMoreBtnRef = ref<HTMLElement | null>(null)
const showAll = ref(false)

const displayedRecommendations = computed(() => {
  return showAll.value ? recommendations : recommendations.slice(0, 2)
})

const hasMoreRecommendations = computed(() => {
  return recommendations.length > 2
})

// Initialize scroll animations
useScrollAnimation(sectionHeaderRef, { threshold: 0.2 })
useScrollAnimation(containerRef, { threshold: 0.1 })
useScrollAnimation(showMoreBtnRef, { threshold: 0.3 })
</script>

<style scoped>
.recommendations-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 43px;
  width: 100%;
  max-width: 1085px;
  margin: 0 auto;
  padding: 6rem 0rem;
}

.section-title {
  width: 100%;
  text-align: center;
  font-family: Inter, -apple-system, Roboto, Helvetica, sans-serif;
  font-size: 52px;
  font-weight: 700;
  line-height: normal;
  background: var(--gradient-accent-side);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin: 0;
}

.recommendations-container {
  display: flex;
  flex-direction: column;
  gap: 24px;
  width: 100%;
}

.recommendation-card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 47.707px 31.805px;
  border-radius: 11.132px;
  border: 1.59px solid var(--linear-top-right);
  background: var(--linear-top-right-fill);
  min-height: 253px;
}

.card-content {
  display: flex;
  align-items: center;
  gap: 16px;
  flex-wrap: wrap;
}

.linkedin-card{
  text-decoration: none;
}

.profile-image {
  width: 84px;
  height: 84px;
  border-radius: 50%;
  flex-shrink: 0;
  object-fit: cover;
}

.profile-info {
  display: flex;
  flex-direction: column;
  gap: 6.361px;
  min-width: 240px;
  flex-shrink: 0;
}

.profile-name {
  color: var(--color-heading);
  font-family: Inter, -apple-system, Roboto, Helvetica, sans-serif;
  font-size: 25px;
  font-weight: 700;
  line-height: normal;
  margin: 0;
}

.profile-link {
  color: inherit;
  text-decoration: none;
  transition: opacity 0.3s ease;
}

.profile-link:hover {
  opacity: 0.8;
  text-decoration: underline;
}

.profile-title {
  color: var(--color-text);
  opacity: 0.7;
  font-family: Inter, -apple-system, Roboto, Helvetica, sans-serif;
  font-size: 16px;
  line-height: normal;
  margin: 0;
}

.title-role {
  font-weight: 700;
}

.title-org {
  font-weight: 400;
}

.recommendation-text {
  color: var(--color-text);
  opacity: 0.75;
  font-family: Inter, -apple-system, Roboto, Helvetica, sans-serif;
  font-weight: 700;
  line-height: normal;
  flex: 1;
  min-width: 280px;
  margin: 0;
}

.show-more-btn {
  display: flex;
  padding: 4.374px;
  justify-content: center;
  align-items: center;
  gap: 4.374px;
  width: 193px;
  border-radius: 12.012px;
  background: var(--gradient-accent-overlay);
  color: var(--color-text);
  font-family: Inter, -apple-system, Roboto, Helvetica, sans-serif;
  font-size: 23px;
  font-weight: 700;
  line-height: normal;
  border: none;
  cursor: pointer;
  transition: opacity 0.3s ease;
}

.show-more-btn:hover {
  opacity: 0.9;
}

.show-more-btn:active {
  opacity: 0.8;
}

/* Large screens */
@media (min-width: 2560px) {
  .section-title {
    font-size: 72px;
  }

  .recommendation-card {
    padding: 60px 40px;
  }

  .profile-image {
    width: 120px;
    height: 120px;
  }

  .profile-name {
    font-size: 32px;
  }

  .profile-title {
    font-size: 20px;
  }

  .recommendation-text {
    font-size: 18px;
  }

  .show-more-btn {
    font-size: 28px;
    width: 240px;
  }
}

/* Tablet and smaller desktops */
@media (max-width: 1440px) {
  .section-title {
    font-size: 48px;
  }

  .recommendation-card {
    padding: 40px 28px;
  }

  .profile-name {
    font-size: 22px;
  }

  .profile-title {
    font-size: 15px;
  }

}

/* Tablet */
@media (max-width: 768px) {
  .recommendations-section {
    gap: 32px;
    padding: 4rem 0rem;
  }

  .section-title {
    font-size: 36px;
    text-align: center;
  }

  .recommendation-card {
    padding: 32px 24px;
    min-height: auto;
  }

  .card-content {
    flex-direction: column;
    align-items: flex-start;
  }

  .profile-info {
    min-width: auto;
    width: 100%;
  }

  .profile-name {
    font-size: 20px;
  }

  .profile-title {
    font-size: 14px;
  }

  .recommendation-text {
    min-width: auto;
    width: 100%;
  }

  .show-more-btn {
    font-size: 20px;
    width: 170px;
  }
}

/* Mobile */
@media (max-width: 425px) {
  .recommendations-section {
    gap: 24px;
    padding: 4rem 1rem;
  }

  .section-title {
    font-size: 28px;
    text-align: center;
  }

  .recommendation-card {
    padding: 24px 20px;
  }

  .profile-image {
    width: 70px;
    height: 70px;
  }

  .profile-name {
    font-size: 18px;
  }

  .profile-title {
    font-size: 13px;
  }

  .recommendation-text {
    line-height: 1.4;
  }

  .show-more-btn {
    font-size: 18px;
    width: 150px;
    padding: 8px;
  }
}
</style>
