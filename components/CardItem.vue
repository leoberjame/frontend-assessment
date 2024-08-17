<template>
  <div class="card custom__card simple__shadow p-4">
    <slot name="card-img" />
    <div
      class="
        card-body
        d-flex
        flex-column
        justify-content-between
        align-items-center
        text-center
        p-0
      "
    >
      <p class="card-text">
        <slot name="card-info" />
      </p>
      <a href="#" class="btn custom__btn text-uppercase">
        <slot name="card-button" />
      </a>
    </div>
  </div>
</template>
<script>
export default {
  name: 'CardItem',
}
</script>