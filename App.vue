<template>
  <div class="flex h-screen overflow-hidden bg-gray-100">
    <Sidebar
      :curSettings="curSettings"
      :showSideBar="showSideBar"
      @update:showSideBar="showSideBar = !showSideBar"
    />

    <div class="flex flex-col flex-1 w-0 overflow-hidden">
      <nav class="bg-gray-800">
        <div class="px-4 mx-auto max-w-7xl sm:px-6 lg:px-8">
          <div class="flex items-center justify-between h-16">
            <div class="flex items-center">
              <button
                @click="showSideBar = !showSideBar"
                class="px-4 text-gray-500 border-gray-200 focus:outline-none focus:text-gray-600"
                aria-label="Open sidebar"
              >
                <svg
                  class="w-6 h-6"
                  stroke="currentColor"
                  fill="none"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M4 6h16M4 12h16M4 18h7"
                  />
                </svg>
              </button>
              <div class="hidden md:block">
                <div class="flex items-baseline ml-10">
                  <router-link
                    v-for="(link, i) in links"
                    :key="i"
                    v-slot="{ navigate, href, isExactActive }"
                    :to="link.to"
                  >
                    <a
                      :href="href"
                      class="px-3 py-2 text-sm font-medium rounded-md"
                      :class="[
                        isExactActive
                          ? 'text-white bg-gray-900 focus:outline-none focus:text-white focus:bg-gray-700'
                          : 'text-gray-300 hover:text-white hover:bg-gray-700 focus:outline-none focus:text-white focus:bg-gray-700',
                        i > 0 && 'ml-4',
                      ]"
                      @click="navigate"
                      >{{ link.text }}</a
                    >
                  </router-link>
                </div>
              </div>
            </div>
            <div class="hidden md:block">
              <div class="flex items-center ml-4 md:ml-6">
                <button
                  class="p-1 text-gray-400 border-2 border-transparent rounded-full hover:text-white focus:outline-none focus:text-white focus:bg-gray-700"
                  aria-label="Notifications"
                >
                  <svg
                    class="w-6 h-6"
                    stroke="currentColor"
                    fill="none"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
                    />
                  </svg>
                </button>

                <!-- Profile dropdown -->
                <div class="relative ml-3">
                  <div>
                    <button
                      id="user-menu"
                      class="flex items-center max-w-xs text-sm text-white rounded-full focus:outline-none focus:shadow-solid"
                      aria-label="User menu"
                      aria-haspopup="true"
                      @click="showProfileMenu = !showProfileMenu"
                    >
                      <img
                        class="w-8 h-8 rounded-full"
                        src="/img/person1.jpeg"
                        alt
                      />
                    </button>
                  </div>

                  <transition
                    enter-active-class="transition duration-100 ease-out"
                    enter-from-class="transform scale-95 opacity-0"
                    enter-to-class="transform scale-100 opacity-100"
                    leave-active-class="transition duration-75 ease-in"
                    leave-from-class="transform scale-100 opacity-100"
                    leave-to-class="transform scale-95 opacity-0"
                  >
                    <div
                      v-if="showProfileMenu"
                      class="absolute right-0 w-48 mt-2 origin-top-right rounded-md shadow-lg"
                    >
                      <div
                        class="py-1 bg-white rounded-md shadow-xs"
                        role="menu"
                        aria-orientation="vertical"
                        aria-labelledby="user-menu"
                      >
                        <router-link
                          v-for="(link, i) in sideLinks"
                          :key="'x' + i"
                          v-slot="{ navigate, href, isExactActive }"
                          :to="link.to"
                        >
                          <a
                            :href="href"
                            class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
                            role="menuitem"
                            @click="
                              navigate().then(() => (showProfileMenu = false))
                            "
                            >{{ link.text }}</a
                          >
                        </router-link>
                      </div>
                    </div>
                  </transition>
                </div>
              </div>
            </div>

            <div class="flex -mr-2 md:hidden">
              <!-- Mobile menu button -->
              <button
                class="inline-flex items-center justify-center p-2 text-gray-400 rounded-md hover:text-white hover:bg-gray-700 focus:outline-none focus:bg-gray-700 focus:text-white"
                @click="showMenu = !showMenu"
              >
                <!-- Menu open: "hidden", Menu closed: "block" -->
                <svg
                  :class="!showMenu ? 'block' : 'hidden'"
                  class="w-6 h-6"
                  stroke="currentColor"
                  fill="none"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M4 6h16M4 12h16M4 18h16"
                  />
                </svg>
                <!-- Menu open: "block", Menu closed: "hidden" -->
                <svg
                  :class="showMenu ? 'block' : 'hidden'"
                  class="w-6 h-6"
                  stroke="currentColor"
                  fill="none"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M6 18L18 6M6 6l12 12"
                  />
                </svg>
              </button>
            </div>
          </div>
        </div>

        <!--
      Mobile menu, toggle classes based on menu state.

      Open: "block", closed: "hidden"
        -->
        <div class="md:hidden" :class="showMenu ? 'block' : 'hidden'">
          <div class="px-2 pt-2 pb-3 sm:px-3">
            <router-link
              v-for="(link, i) in links"
              :key="i"
              v-slot="{ navigate, href, isExactActive }"
              :to="link.to"
            >
              <a
                :href="href"
                class="block px-3 py-2 text-base font-medium rounded-md"
                :class="[
                  isExactActive
                    ? 'text-white bg-gray-900 focus:outline-none focus:text-white focus:bg-gray-700'
                    : 'text-gray-300 hover:text-white hover:bg-gray-700 focus:outline-none focus:text-white focus:bg-gray-700',
                  i > 0 && 'mt-1',
                ]"
                @click="navigate().then(() => (showMenu = false))"
                >{{ link.text }}</a
              >
            </router-link>
          </div>
          <div class="pt-4 pb-3 border-t border-gray-700">
            <div class="flex items-center px-5">
              <div class="flex-shrink-0">
                <img
                  class="w-10 h-10 rounded-full"
                  src="/img/person1.jpeg"
                  alt
                />
              </div>
              <div class="ml-3">
                <div class="text-base font-medium leading-none text-white">
                  Tom Cook
                </div>
                <div
                  class="mt-1 text-sm font-medium leading-none text-gray-400"
                >
                  tom@example.com
                </div>
              </div>
            </div>
            <div class="px-2 mt-3">
              <router-link
                v-for="(link, i) in sideLinks"
                :key="'x' + i"
                v-slot="{ navigate, href, isExactActive }"
                :to="link.to"
              >
                <a
                  :href="href"
                  class="block px-3 py-2 mt-1 text-base font-medium text-gray-400 rounded-md hover:text-white hover:bg-gray-700 focus:outline-none focus:text-white focus:bg-gray-700"
                  @click="navigate().then(() => (showProfileMenu = false))"
                  >{{ link.text }}</a
                >
              </router-link>
            </div>
          </div>
        </div>
      </nav>

      <header v-if="$route.meta.title" class="bg-white shadow">
        <div class="px-4 py-6 mx-auto max-w-7xl sm:px-6 lg:px-8">
          <h1 class="text-3xl font-bold leading-tight text-gray-900">
            {{ $route.meta.title }}
          </h1>
        </div>
      </header>
      <main class="overflow-auto">
        <Suspense>
          <template #default>
            <router-view />
          </template>
          <template #fallback>
            <div>Loading...</div>
          </template>
        </Suspense>
      </main>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue"
import Sidebar from "./components/Sidebar.vue"

export default defineComponent({
  components: {
    Sidebar,
  },
  computed: {
    curSettings() {
      return { name: "Huseyn" }
    },
  },
  mounted() {
    console.log("Hello", this)
  },
  data: () => ({
    showSideBar: true,
    showMenu: false,
    showProfileMenu: false,
    sideLinks: [
      { text: "User", to: "/user" },
      { text: "About", to: "/about" },
      { text: "Signout", to: "/" },
    ],
    links: [
      { text: "Home", to: "/" },
      { text: "About", to: "/about" },
      { text: "Lettings", to: "/lettings" },
    ],
  }),
})
</script>
