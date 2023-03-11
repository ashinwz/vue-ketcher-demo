<template>
  <div :class="darkMode ? 'dark' : ''">
    <TransitionRoot as="template" :show="sidebarOpen">
      <Dialog
        as="div"
        class="relative z-40 md:hidden"
        @close="sidebarOpen = false"
      >
        <TransitionChild
          as="template"
          enter="transition-opacity ease-linear duration-300"
          enter-from="opacity-0"
          enter-to="opacity-100"
          leave="transition-opacity ease-linear duration-300"
          leave-from="opacity-100"
          leave-to="opacity-0"
        >
          <div class="fixed inset-0 bg-gray-600 bg-opacity-75" />
        </TransitionChild>

        <div class="fixed inset-0 z-40 flex">
          <TransitionChild
            as="template"
            enter="transition ease-in-out duration-300 transform"
            enter-from="-translate-x-full"
            enter-to="translate-x-0"
            leave="transition ease-in-out duration-300 transform"
            leave-from="translate-x-0"
            leave-to="-translate-x-full"
          >
            <DialogPanel
              class="relative flex w-full max-w-xs flex-1 flex-col bg-gray-800 pt-5 pb-4"
            >
              <TransitionChild
                as="template"
                enter="ease-in-out duration-300"
                enter-from="opacity-0"
                enter-to="opacity-100"
                leave="ease-in-out duration-300"
                leave-from="opacity-100"
                leave-to="opacity-0"
              >
                <div class="absolute top-0 right-0 -mr-12 pt-2">
                  <button
                    type="button"
                    class="ml-1 flex h-10 w-10 items-center justify-center rounded-full focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white"
                    @click="sidebarOpen = false"
                  >
                    <span class="sr-only">Close sidebar</span>
                    <XMarkIcon class="h-6 w-6 text-white" aria-hidden="true" />
                  </button>
                </div>
              </TransitionChild>
              <div class="flex flex-shrink-0 items-center px-4">
                <img
                  class="h-8 w-auto"
                  src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=500"
                  alt="Your Company"
                />
              </div>
              <div class="mt-5 h-0 flex-1 overflow-y-auto">
                <nav class="space-y-1 px-2">
                  <a
                    v-for="item in navigation"
                    :key="item.name"
                    :href="item.href"
                    :class="[
                      item.current
                        ? 'bg-gray-900 text-white'
                        : 'text-gray-300 hover:bg-gray-700 hover:text-white',
                      'group flex items-center px-2 py-2 text-base font-medium rounded-md',
                    ]"
                  >
                    <component
                      :is="item.icon"
                      :class="[
                        item.current
                          ? 'text-gray-300'
                          : 'text-gray-400 group-hover:text-gray-300',
                        'mr-4 flex-shrink-0 h-6 w-6',
                      ]"
                      aria-hidden="true"
                    />
                    <p>{{ item.name }}</p>
                  </a>
                </nav>
              </div>
              <div
                class="flex border-t px-3 py-3 justify-between"
                :class="[sidebarSmall ? '' : 'hidden']"
              >
                <a href="#" class="group block">
                  <div class="flex items-center">
                    <div>
                      <img
                        class="inline-block h-10 w-10 rounded-full"
                        src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
                        alt=""
                      />
                    </div>
                    <div class="ml-3">
                      <p class="text-base font-medium text-white">Tom Cook</p>
                      <p
                        class="text-sm font-medium text-indigo-200 group-hover:text-white"
                      >
                        View profile
                      </p>
                    </div>
                  </div>
                </a>
                <a
                  href="#"
                  class="text-white hover:bg-gray-700 hover:bg-opacity-75 group flex items-center px-2 py-2 text-base font-medium rounded-md"
                >
                  <!-- Heroicon name: outline/folder -->
                  <ArrowRightOnRectangleIcon
                    class="h-6 w-6"
                    aria-hidden="true"
                  />
                </a>
              </div>
            </DialogPanel>
          </TransitionChild>
          <div class="w-14 flex-shrink-0" aria-hidden="true">
            <!-- Dummy element to force sidebar to shrink to fit close icon -->
          </div>
        </div>
      </Dialog>
    </TransitionRoot>

    <!-- Static sidebar for desktop -->
    <div
      class="hidden md:fixed md:inset-y-0 md:flex md:w-64 md:flex-col"
      :class="[sidebarSmall ? '' : 'md:w-[60px]']"
    >
      <!-- Sidebar component, swap this element with another sidebar if you like -->
      <div
        class="flex min-h-0 flex-1 flex-col bg-white dark:bg-gray-900 border-r dark:border-gray-700"
      >
        <div class="flex h-16 flex-shrink-0 items-center px-4">
          <img
            class="h-8"
            :class="[sidebarSmall ? 'w-8' : 'w-auto']"
            src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=500"
            alt="Your Company"
          />
          <router-link
            to="/Modal"
            class="pl-4 font-medium text-black dark:text-white"
          >
            Ketcher Demo
          </router-link>
        </div>
        <div class="flex flex-1 flex-col overflow-y-auto dark:bg-gray-800">
          <nav class="flex-1 space-y-1 px-2 py-4">
            <router-link
              v-for="item in navigation"
              :key="item.name"
              :href="item.href"
              :to="item.name"
              class="text-gray-500 dark:text-gray-500 focus:bg-gray-200 dark:focus:bg-gray-600 group-focus:text-gray-800 dark:group-focus:text-white focus:text-gray-800 hover:bg-gray-100 hover:text-gray-800 dark:hover:bg-gray-700 dark:hover:text-white group flex items-center px-2 py-2 text-sm font-medium rounded-md"
              :class="[
                this.$route.name === item.name
                  ? 'bg-gray-200 text-gray-800 dark:bg-gray-600 dark:text-white dark:focus:text-white '
                  : '',
              ]"
            >
              <component
                :is="item.icon"
                class="h-6 w-6"
                aria-hidden="true"
                :class="[
                  this.$route.name === item.name ? 'dark:text-white' : '',
                ]"
              />
              <p
                class=""
                :class="[
                  sidebarSmall ? 'ml-4' : 'hidden',
                  this.$route.name === item.name ? 'dark:text-white' : '',
                ]"
              >
                {{ item.name }}
              </p>
            </router-link>
          </nav>
        </div>
        <div class="flex px-3 py-3 justify-between">
          <a
            href="#"
            class="group block"
            :class="[sidebarSmall ? '' : 'hidden']"
          >
            <div class="flex items-center">
              <div>
                <img
                  class="inline-block h-10 w-10 rounded-full"
                  src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
                  alt=""
                />
              </div>
              <div class="ml-3">
                <p class="text-base font-medium text-black dark:text-gray-300">
                  Tom Cook
                </p>
                <p
                  class="text-sm font-medium text-black dark:text-gray-300 group-hover:text-black: dark:group-hover:text-white"
                >
                  View profile
                </p>
              </div>
            </div>
          </a>
          <a
            href="#"
            class="text-gray-400 dark:text-white hover:bg-black hover:bg-opacity-75 group flex items-center px-2 py-2 text-base font-medium rounded-md"
          >
            <!-- Heroicon name: outline/folder -->
            <ArrowRightOnRectangleIcon class="h-6 w-6" aria-hidden="true" />
          </a>
        </div>
      </div>
    </div>
    <div class="h-full" :class="[sidebarSmall ? 'md:pl-64' : 'md:pl-[60px]']">
      <div class="sticky top-0 z-5 flex h-16 flex-shrink-0 bg-white shadow">
        <button
          type="button"
          class="border-r dark:bg-gray-700 border-gray-200 px-4 text-gray-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500 md:hidden"
          @click="sidebarOpen = true"
        >
          <span class="sr-only">Open sidebar</span>
          <Bars3CenterLeftIcon class="h-6 w-6" aria-hidden="true" />
        </button>
        <div
          class="flex flex-1 justify-between bg-white dark:bg-gray-900 dark:border-gray-200"
        >
          <div
            class="flex items-center h-full bg-white dark:bg-gray-900 dark:hover:bg-gray-700 hover:text-white border-r dark:border-gray-700 max-md:hidden"
          >
            <button
              @click="sidebarSmall = false"
              class="border-gray-200 px-4 text-gray-500 focus:outline-none"
              :class="[sidebarSmall ? '' : 'hidden']"
            >
              <Bars3BottomLeftIcon
                class="h-8 w-8 text-gray-400 hover:rotate-180 duration-500"
                aria-hidden="true"
              />
            </button>

            <button
              @click="sidebarSmall = true"
              class="border-gray-200 dark:border-gray-700 px-4 text-gray-500 focus:outline-none"
              :class="[sidebarSmall ? 'hidden' : '']"
            >
              <Bars3BottomRightIcon
                class="h-8 w-8 text-gray-400 hover:rotate-180 duration-500"
                aria-hidden="true"
              />
            </button>
          </div>
          <div class="flex flex-1 px-3 bg-white dark:bg-gray-900">
            <form class="flex w-full md:ml-0" action="#" method="GET">
              <label for="search-field" class="sr-only">Search</label>
              <div
                class="relative w-full text-gray-400 focus-within:text-gray-600"
              >
                <div
                  class="pointer-events-none absolute inset-y-0 left-0 flex items-center"
                >
                  <MagnifyingGlassIcon class="h-5 w-5" aria-hidden="true" />
                </div>
                <input
                  id="search-field"
                  class="bg-white dark:bg-gray-900 dark:text-white block h-full w-full border-transparent py-2 pl-8 pr-3 text-gray-900 placeholder-gray-500 focus:border-transparent focus:placeholder-gray-400 focus:outline-none focus:ring-0 sm:text-sm"
                  placeholder="Search"
                  type="search"
                  name="search"
                />
              </div>
            </form>
          </div>
          <div class="ml-4 mr-4 flex items-center md:ml-6">
            <button
              type="button"
              @click="darkMode = true"
              class="relative mr-3 rounded-full bg-white dark:bg-gray-900 p-1 text-gray-400 dark:text-white hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
              :class="darkMode ? 'hidden' : ''"
            >
              <span class="sr-only">moon</span>
              <MoonIcon class="h-6 w-6" aria-hidden="true" />
            </button>

            <button
              type="button"
              @click="darkMode = false"
              class="relative mr-3 rounded-full bg-white dark:bg-gray-900 p-1 text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
              :class="darkMode ? '' : 'hidden'"
            >
              <span class="sr-only">sun</span>
              <SunIcon class="h-6 w-6" aria-hidden="true" />
            </button>

            <button
              type="button"
              class="rounded-full bg-white p-1 text-gray-400 dark:bg-gray-900 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
            >
              <span class="sr-only">View notifications</span>
              <BellIcon class="h-6 w-6" aria-hidden="true" />
            </button>

            <!-- Profile dropdown -->
            <Menu as="div" class="relative ml-3">
              <div>
                <MenuButton
                  class="flex max-w-xs items-center rounded-full bg-white text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                >
                  <span class="sr-only">Open user menu</span>
                  <img
                    class="h-8 w-8 rounded-full"
                    src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
                    alt=""
                  />
                </MenuButton>
              </div>
              <transition
                enter-active-class="transition ease-out duration-100"
                enter-from-class="transform opacity-0 scale-95"
                enter-to-class="transform opacity-100 scale-100"
                leave-active-class="transition ease-in duration-75"
                leave-from-class="transform opacity-100 scale-100"
                leave-to-class="transform opacity-0 scale-95"
              >
                <MenuItems
                  class="absolute right-0 z-5 mt-2 w-48 origin-top-right rounded-md bg-white py-1 shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
                >
                  <MenuItem
                    v-for="item in userNavigation"
                    :key="item.name"
                    v-slot="{ active }"
                  >
                    <a
                      :href="item.href"
                      :class="[
                        active ? 'bg-gray-100' : '',
                        'block px-4 py-2 text-sm text-gray-700',
                      ]"
                      >{{ item.name }}</a
                    >
                  </MenuItem>
                </MenuItems>
              </transition>
            </Menu>
          </div>
        </div>
      </div>

      <main class="flex-1 h-[calc(100vh-4rem)] dark:bg-gray-800">
        <div class="py-2 mx-auto">
          <!-- Replace with your content -->
          <!-- <DashboardView /> -->
          <router-view />
          <!-- /End replace -->
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import {
  Dialog,
  DialogPanel,
  Menu,
  MenuButton,
  MenuItem,
  MenuItems,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import {
  Bars3BottomLeftIcon,
  BellIcon,
  CalendarIcon,
  ChartBarIcon,
  FolderIcon,
  HomeIcon,
  InboxIcon,
  UsersIcon,
  XMarkIcon,
  Bars3CenterLeftIcon,
  Bars3BottomRightIcon,
  ArrowRightOnRectangleIcon,
  SunIcon,
  MoonIcon,
} from "@heroicons/vue/24/outline";
import { MagnifyingGlassIcon } from "@heroicons/vue/20/solid";

const navigation = [
  { name: "Modal", href: "#Modal", icon: HomeIcon, current: true }
];
const userNavigation = [
  { name: "Your Profile", href: "#demo" },
  { name: "Settings", href: "#" },
  { name: "Sign out", href: "#" },
];

const sidebarOpen = ref(false);
const sidebarSmall = ref(true);
const darkMode = ref(false);
</script>
