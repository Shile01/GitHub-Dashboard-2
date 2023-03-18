<template>
  <div>
    <div class="container error-design-wrap">
        <h1>404</h1>
        <div className="top-navigation">
           <h2>
            Ohh, Shit
          </h2>
          <p>Page doesn't exist</p>
          <RouterLink to="/" class="">
          <p className="back"><i class="fa-solid fa-circle-left"></i> Go Back Home</p>
        </RouterLink>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NotFoundView'
}
</script>

<style scoped>

.error-design-wrap {
  width: 100%;
  height: 85vh;
  display: grid;
  place-content: center;
  text-align: center;
  color: #002147;
}
.error-design-wrap h1 {
  font-size: 124px;
  color: #002147;
}

.top-navigation {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.back {
  margin-top: 16px;
  border: 1px solid #002147;
  color: #fff;
  text-align: center;
  padding: 16px 32px;
  border-radius: 8px;
  background-color: #002147;
  transform: transform 250ms ease;
}

.back:hover,.back:focus {
  background-color: #fff;
  color: #002147;
  border: 1px solid #002147;
  /* transform: scale(1.05); */
}
</style>
