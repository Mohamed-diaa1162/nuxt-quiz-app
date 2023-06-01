<template>
  <div>
    <div class="card text-white bg-primary mb-3" style="max-width: 18rem">
      <div class="card-header text-center">Os Quiz</div>
      <div class="card-body">
        <div class="card-text text-center">
          <p class="row">
            <nuxt-link
              class="col btn btn-custom m-1 d-flex align-items-center justify-content-center"
              to="/quiz"
            >
              Start
            </nuxt-link>
            <nuxt-link class="col btn btn-custom m-1" to="/quiz?random=1">
              Start With Random Order
            </nuxt-link>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
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
