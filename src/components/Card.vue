<template>
  <div class="card">
    <h1>{{ title }}</h1>
    <p>{{ description }}
      <ul>
        <li><span>Director: </span> {{ director }} </li>
        <li><span>Producer: </span> {{ producer }} </li>
        <li><span>Release: </span> {{ release }} </li>
        <li v-if="characters"><span >Characters: </span>  {{ characters }} </li>
      </ul>
    </p>
  </div>
</template>

<script>
export default {
  props: ['title', 'description', 'director', 'producer', 'release', 'characters']
};
</script>

<style lang="scss">
.card {
  margin: 1rem;
  background: white;
  box-shadow: 2px 4px 25px rgba(0, 0, 0, 0.1);
  border-radius: 12px;
  overflow: hidden;
  transition: all 0.2s linear;

  @include tablet-down {
    flex: 1 1 calc(50% - 2rem);
    max-width: 50%;
  }

  @include desktop-up {
    flex: 1 1 calc(33% - 2rem);
    max-width: 33%;
  }

  & h1 {
    text-align: center;
    padding: 1.5rem 2.5rem;
    background-image: linear-gradient(120deg, #fbc2eb 0%, #a6c1ee 100%);
    margin: 0 0 1.7rem 0;
    font-size: 1.5rem;
    color: white;
    font-weight: 700;
  }

  & p {
    padding: 0 2.5rem 2rem;
    margin: 0;
    line-height: 1.6;
    text-align: left;
    color: $text-color;
  }

  & ul {
    margin-top: 1rem;
  }

  & span {
    font-weight: 700;
  }

  &:hover {
    box-shadow: 2px 8px 45px rgba(0, 0, 0, 0.15);
    transform: translate3D(0, -2px, 0);
  }

  &:nth-child(2n) h1 {
    background-image: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
  }

  &:nth-child(4n) h1 {
    background-image: linear-gradient(120deg, #ff9a9e 0%, #fecfef 100%);
  }

  &:nth-child(5n) h1 {
    background-image: linear-gradient(120deg, #ffc3a0 0%, #ffafbd 100%);
  }
}
</style>