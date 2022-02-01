<template>
  <div>
    <div class="card text-white bg-primary mb-3" style="max-width: 18rem">
      <div class="card-header text-center">Matlab Quiz</div>
      <div class="card-body">
        <p class="card-text text-center">
          To Start Quiz

          <nuxt-link class="btn btn-info" to="/quiz">Go</nuxt-link>
        </p>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.card {
  margin: auto;
  max-width: 90%;
  min-width: 70%;
  margin-top: 20px;
  font-weight: bold;
  font-size: 30px;
  background-color: #f7f7f7 !important;
}
.card-header {
  color: #1f2639;
}
.card-body .blockquote {
  background-color: #f7f7f7 !important;
}
.result {
  color: #1bff1b;
  font-weight: bold;
}
</style>
