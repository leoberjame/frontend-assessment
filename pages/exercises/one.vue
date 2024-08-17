<template>
  <section
    class="justify-content-center align-items-center list__container py-5"
  >
    <CardItem v-for="(card, index) in cardList" :key="`card-item-${index}`">
      <img
        :src="`${card.img}`"
        @load="onError()"
        :class="[`card-img-top`, { skeleton: imgLoadingState }]"
        alt="card img"
        slot="card-img"
      />
      <template #card-info>
        {{ card.info }}
      </template>
      <template #card-button>
        <span @mousemove="onMouseHover($event)">
          {{ card.btnTxt }}
        </span>
      </template>
    </CardItem>
  </section>
</template>
<script>
export default {
  name: 'ExerciseOne',
  layout: 'Exercise',
  data() {
    return {
      cardList: [
        {
          img: 'https://via.placeholder.com/400x300',
          info: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
          url: '#',
          btnTxt: 'read more',
        },
        {
          img: 'https://via.placeholder.com/400x300',
          info: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
          url: '#',
          btnTxt: 'read more',
        },
        {
          img: 'https://via.placeholder.com/400x300',
          info: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco.',
          url: '#',
          btnTxt: 'read more',
        },
      ],
      imgLoadingState: true,
      hasImgError: false,
    }
  },
  methods: {
    onError() {
      this.imgLoadingState = true
      this.hasImgError = !this.hasImgError
      setTimeout(() => {
        this.imgLoadingState = false
      }, 400)
    },
    onMouseHover(e) {
      const x = e.pageX - e.target.offsetLeft
      const y = e.pageY - e.target.offsetTop

      e.target.style.setProperty('--x', x + 'px')
      e.target.style.setProperty('--y', y + 'px')
    },
  },
}
</script>