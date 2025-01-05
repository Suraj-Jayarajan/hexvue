<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Greeting from './components/Greeting.vue'
import Menubar from 'primevue/menubar';
import PanelMenu from 'primevue/panelmenu';
import Panel from 'primevue/panel';
import Column from 'primevue/column';
import DataTable from 'primevue/datatable';
import Divider from 'primevue/divider';
import Button from 'primevue/button';
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

const items = ref([
  {
    label: 'Home',
    icon: 'pi pi-home'
  },
  {
    label: 'About',
    icon: 'pi pi-info-circle'
  }
]);



const sidebarItems = ref([
  {
    label: 'Clients',
    icon: 'pi pi-file-check',
    items: [
      {
        label: 'Styled',
        icon: 'pi pi-eraser',
        route: '/theming/styled'
      },
      {
        label: 'Unstyled',
        icon: 'pi pi-heart',
        route: '/theming/unstyled'
      }
    ]
  },
  {
    label: 'Packs & Mixes',
    icon: 'pi pi-box',
    command: () => {
      router.push('/introduction');
    }
  },
  {
    label: 'Settings',
    icon: 'pi pi-cog',
    items: [
      {
        label: 'Vue.js',
        icon: 'pi pi-star',
        url: 'https://vuejs.org/'
      },
      {
        label: 'Vite.js',
        icon: 'pi pi-bookmark',
        url: 'https://vuejs.org/'
      }
    ]
  }
]);

const clients = ref([
  {
    commercial_name: "ABC Corp",
    are_locals_approved: true,
    working: true,
    active: true,
  },
  {
    commercial_name: "XYZ LLC",
    are_locals_approved: false,
    working: false,
    active: true,
  },
  {
    commercial_name: "Acme Ltd",
    are_locals_approved: true,
    working: true,
    active: false,
  },
  {
    commercial_name: "Global Co",
    are_locals_approved: false,
    working: true,
    active: true,
  },
])

</script>

<template>
  <div class="grid grid-cols-5 grid-rows-[auto_1fr] gap-4 h-full">
    <header class="col-span-full h-">
      <Menubar :model="items">
        <template #start>
          <img src="./assets/logo3.png" class="" />
          <!-- <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 512 512">
            <path fill="#00bd7e"
              d="m256 21.52l-4.5 2.597L52.934 138.76v234.48L256 490.48l203.066-117.24V138.76zm0 20.783l185.066 106.85v213.695L256 469.698L70.934 362.847V149.152L256 42.302zm0 30.93l-4.5 2.597l-153.78 88.785v182.77L256 438.768l158.28-91.383v-182.77L256 73.232zm0 20.783l140.28 80.992v161.984L256 417.984l-140.28-80.992V175.008zm0 30.93l-4.5 2.597l-108.998 62.93v131.054L256 387.055l113.498-65.528V190.473L256 124.945zm0 20.783l95.498 55.135v110.27L256 366.27l-95.498-55.135v-110.27zm0 30.928l-4.5 2.598l-64.213 37.072v79.344L256 335.342l68.713-39.67v-79.344zm0 20.783l50.713 29.28v58.56L256 314.56l-50.713-29.28v-58.56zm0 30.93l-4.5 2.6l-19.428 11.216v27.628L256 283.63l23.928-13.816v-27.628z" />
          </svg> -->
          <Divider type="vertical" />
        </template>
      </Menubar>
    </header>

    <aside class="h-full hidden lg:block lg:col-span-1">
      <Panel header="Sidebar" class="h-full">
        <PanelMenu :model="sidebarItems" class="w-full">
          <template #item="{ item }">
            <router-link v-if="item.route" v-slot="{ href, navigate }" :to="item.route" custom>
              <a v-ripple class="flex items-center cursor-pointer text-surface-700 dark:text-surface-0 px-4 py-2"
                :href="href" @click="navigate">
                <span :class="item.icon" />
                <span class="ml-2">{{ item.label }}</span>
              </a>
            </router-link>
            <a v-else v-ripple class="flex items-center cursor-pointer text-surface-700 dark:text-surface-0 px-4 py-2"
              :href="item.url" :target="item.target">
              <span :class="item.icon" />
              <span class="ml-2">{{ item.label }}</span>
              <span v-if="item.items" class="pi pi-angle-down text-primary ml-auto" />
            </a>
          </template>
        </PanelMenu>
      </Panel>
    </aside>

    <main class="col-span-full lg:col-span-4 h-full">
      <Panel header="Clients">
        <div class="grid grid-cols-6 gap-2">
          <div class="col-span-full lg:col-span-4">
            <DataTable :value="clients" showGridlines stripedRows >
              <Column field="commercial_name" header="Commercial Name"></Column>
              <Column field="are_locals_approved" header="Are Locals Approved?"></Column>
              <Column field="working" header="Working"></Column>
              <Column field="active" header="Active"></Column>
              <Column field="actions" header="">
                <template #body="{ data }">
                  <Button icon="pi pi-pencil" severity="contrast" text rounded aria-label="Edit" />
                </template>
              </Column>
              <template #empty>No Results</template>
            </DataTable>
          </div>
          <div class="col-span-full lg:col-span-2 h-full">
            <Panel header="Rooms" class="h-full">

            </Panel>
          </div>
        </div>

      </Panel>
    </main>
  </div>



  <RouterView />
</template>

<style scoped></style>
