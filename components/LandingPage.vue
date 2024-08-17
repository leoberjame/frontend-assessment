<template>
  <div class="vh-100 landing__bg w-100">
    <div class="overlay__blur"></div>

    <div class="wrapper">
      <NuxtLink :class="[``, {}]" :to="{ path: '/exercises/one' }">
        <div class="card card__0">
          <div class="glare__container">
            <div class="glare"></div>
          </div>
          <h1 class="title text-center">Exercise 1</h1>
        </div>
      </NuxtLink>

      <NuxtLink :class="[``, {}]" :to="{ path: '/exercises/two' }">
        <div class="card card__1">
          <div class="glare__container">
            <div class="glare"></div>
          </div>
          <h1 class="title text-center">Exercise 2</h1>
        </div>
      </NuxtLink>
    </div>
  </div>
</template>
<script>
export default {
  name: 'LandingPage',
  mounted() {
    const limits = 15.0
    this.addCardEvents(limits)
  },
  beforeDestroy() {
    this.removeCardEvents()
  },
  methods: {
    addCardEvents(limits) {
      document.querySelectorAll('.card').forEach((card) => {
        card.addEventListener('mousemove', (e) => {
          const rect = e.target.getBoundingClientRect()
          const x = e.clientX - rect.left //x position within the element.
          const y = e.clientY - rect.top //y position within the element.
          const offsetX = x / rect.width
          const offsetY = y / rect.height

          const rotateY = offsetX * (limits * 2) - limits
          const rotateX = offsetY * (limits * 2) - limits

          const shadowOffsetX = offsetX * 32 - 16
          const shadowOffsetY = offsetY * 32 - 16

          card.style.boxShadow = `${(1 / 6) * -shadowOffsetX}px 
        ${(1 / 6) * -shadowOffsetY}
        px 3px rgba(0, 0, 0, 0.051),
        ${(2 / 6) * -shadowOffsetX}px 
        ${(2 / 6) * -shadowOffsetY}
        px 7.2px rgba(0, 0, 0, 0.073),
        ${(3 / 6) * -shadowOffsetX}px 
        ${(3 / 6) * -shadowOffsetY}
        px 13.6px rgba(0, 0, 0, 0.09),
        ${(4 / 6) * -shadowOffsetX}px 
        ${(4 / 6) * -shadowOffsetY}
        px 24.3px rgba(0, 0, 0, 0.107),
        ${(5 / 6) * -shadowOffsetX}px 
        ${(5 / 6) * -shadowOffsetY}
        px 45.5px rgba(0, 0, 0, 0.129),
        ${-shadowOffsetX}px ${-shadowOffsetY}px 109px rgba(0, 0, 0, 0.18)`

          card.style.transform = `perspective(1000px) rotateX(${-rotateX}deg) rotateY(${rotateY}deg)`
          card.style.transition = 'none'

          const glarePos = rotateX + rotateY + 90
          card.querySelector('.glare').style.left = `${glarePos}%`
        })

        card.addEventListener('mouseleave', (e) => {
          card.style.boxShadow =
            '0px 0px 3px rgba(0, 0, 0, 0.051), 0px 0px 7.2px rgba(0, 0, 0, 0.073), 0px 0px 13.6px rgba(0, 0, 0, 0.09), 0px 0px 24.3px rgba(0, 0, 0, 0.107), 0px 0px 45.5px rgba(0, 0, 0, 0.129), 0px 0px 109px rgba(0, 0, 0, 0.18)'
          card.style.transform = 'scale(1.0)'
          card.style.transition = 'transform 1s ease'
          card.querySelector('.glare').style.left = '100%'
        })
      })
    },
    removeCardEvents() {
      document.querySelectorAll('.card').forEach((card) => {
        card.removeEventListener('mousemove', (e) => {})

        card.removeEventListener('mouseleave', (e) => {})
      })
    },
  },
}
</script>
