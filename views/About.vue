<template>
  <main>
    <div class="py-6 mx-auto max-w-7xl sm:px-6 lg:px-8">
      <div class="px-4 py-6 sm:px-0">
        <div
          class="max-w-screen-xl px-4 mx-auto mt-10 sm:mt-12 sm:px-6 md:mt-16 lg:mt-20 lg:px-8 xl:mt-28"
        >
          <div class="sm:text-center lg:text-left">
            <h2
              class="text-4xl font-extrabold leading-10 tracking-tight text-gray-900 sm:text-5xl sm:leading-none md:text-6xl"
            >
              This demo is using
              <br class="xl:hidden" />
              <a
                target="_blank"
                class="text-indigo-600 underline hover:text-indigo-500"
                href="https://tailwindcss.com"
                >Tailwind CSS</a
              >
            </h2>
            <p
              class="mt-3 text-base text-gray-500 sm:mt-5 sm:text-lg sm:max-w-xl sm:mx-auto md:mt-5 md:text-xl lg:mx-0"
            >
              All the code present here is part of a free sample from
              <a
                href="https://tailwindui.com"
                class="text-indigo-600 underline hover:text-indigo-500"
                >Tailwind UI</a
              >
              but, you don't need it. There is also a version configured to use
              <b>Tailwind UI </b>&#32;
              <a
                class="text-indigo-600 underline hover:text-indigo-500"
                href="https://github.com/posva/vite-tailwind-starter/tree/tailwind-ui"
                >in a different branch</a
              >
            </p>
            <div
              class="mt-5 sm:mt-8 sm:flex sm:justify-center lg:justify-start"
            >
              <div class="rounded-md shadow">
                <a
                  href="https://github.com/posva/vite-tailwind-starter"
                  class="flex items-center justify-center w-full px-8 py-3 text-base font-medium leading-6 text-white transition duration-150 ease-in-out bg-indigo-600 border border-transparent rounded-md hover:bg-indigo-500 focus:outline-none focus:shadow-outline md:py-4 md:text-lg md:px-10"
                >
                  Get started
                </a>
              </div>
              <div class="mt-3 sm:mt-0 sm:ml-3">
                <a
                  href="#"
                  class="flex items-center justify-center w-full px-8 py-3 text-base font-medium leading-6 text-indigo-700 transition duration-150 ease-in-out bg-indigo-100 border border-transparent rounded-md hover:text-indigo-600 hover:bg-indigo-50 focus:outline-none focus:shadow-outline focus:border-indigo-300 md:py-4 md:text-lg md:px-10"
                >
                  Live demo
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <br />
  </main>
</template>

<script>
export default {
  data: cx => {
    console.log(cx)
    return {}
  },
}
</script>
