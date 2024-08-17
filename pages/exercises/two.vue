<template>
  <div class="container-fluid vh-100">
    <div
      class="d-flex justify-content-center align-items-start exercise2 vh-100"
    >
      <div class="container">
        <h1>Responsive Accordion</h1>
        <div class="d-flex flex-wrap">
          <div
            v-for="(tab, index) in arrData"
            :key="`tabs-container-${index}`"
            class="single__container"
          >
            <button class="accordion" @click="setCurrentTab(index)">
              {{ tab.title }}
            </button>
            <div class="panel">
              <div v-html="tab.content"></div>
            </div>
          </div>
        </div>
        <div class="panel__desktop">
          <div
            v-html="arrData[currentTab] ? arrData[currentTab].content : null"
          ></div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import tabList from '@/assets/exercise2/data.json'
export default {
  name: 'ExerciseTwo',
  layout: 'Exercise',
  data() {
    return {
      currentTab: 0,
      isMobile: window.innerWidth <= 768,
    }
  },
  computed: {
    arrData() {
      return [...tabList]
    },
  },
  mounted() {
    if (document.querySelector('.accordion') !== null) {
      const accordion = document.getElementsByClassName('accordion')

      openFirstAccordionTab()
      this.currentTab = 0

      for (let i = 0; i < accordion.length; i++) {
        accordion[i].addEventListener('click', function () {
          if (!this.classList.contains('active')) {
            closeAccordionTabs()
            toggleAccordion(this)
          } else {
            closeAccordionTabs()
          }
        })
      }

      function toggleAccordion(e) {
        e.classList.toggle('active')
        const panel =
          window.innerWidth <= 768
            ? e.nextElementSibling
            : document.querySelector('.panel__desktop')
        if (panel.style.maxHeight) {
          panel.style.maxHeight = null
        } else {
          panel.style.maxHeight = panel.scrollHeight + 'px'
        }
      }

      function closeAccordionTabs() {
        for (let i = 0; i < accordion.length; i++) {
          if (accordion[i].classList.contains('active')) {
            accordion[i].classList.remove('active')
            const panel =
              window.innerWidth <= 768
                ? accordion[i].nextElementSibling
                : document.querySelector('.panel__desktop')
            panel.removeAttribute('style')
            accordion[i].nextElementSibling.removeAttribute('style')
          }
        }
      }

      function openFirstAccordionTab() {
        if (!accordion[0].classList.contains('active')) {
          accordion[0].classList.add('active')
          const panel =
            window.innerWidth <= 768
              ? accordion[0].nextElementSibling
              : document.querySelector('.panel__desktop')
          panel.style.maxHeight = panel.scrollHeight + 'px'
        }
      }

      window.addEventListener(
        'resize',
        function () {
          this.isMobile = window.innerWidth <= 768
          for (let i = 0; i < accordion.length; i++) {
            if (accordion[i].classList.contains('active')) {
              const panel = this.isMobile
                ? accordion[i].nextElementSibling
                : document.querySelector('.panel__desktop')
              panel.style.maxHeight = panel.scrollHeight + 'px'
              accordion[i].nextElementSibling.style.maxHeight =
                accordion[i].nextElementSibling.scrollHeight + 'px'
            }
          }
        },
        true
      )
    }
  },
  methods: {
    setCurrentTab(data) {
      this.currentTab = this.currentTab == data ? null : data
    },
  },
}
</script>