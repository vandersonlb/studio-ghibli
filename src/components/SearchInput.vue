<template>
  <input type="search" class="container__input" :placeholder="placeholder" />
</template>

<script>
export default {
  props: ["placeholder"],
};
</script>

<style lang="scss">
input {
  display: block;
  margin: 0 auto;
  width: 80%;
  max-width: 800px;
  border: 1px solid lighten($text-color, 20);
  border-radius: 20px;
  padding: 0.5rem 1rem;
  color: $text-color;
  outline: none;
  background-color: transparent;

  &::-webkit-search-cancel-button {
    -webkit-appearance: none;
    background-color: $text-color;
    height: 12px;
    width: 12px;
    border-radius: 50%;
    opacity: .7;
  }

  &::placeholder {
    color: $text-color;
    opacity: 0.5;
  }

  &:focus {
    border-color: darken($text-color, 10);
  }
}
</style>
