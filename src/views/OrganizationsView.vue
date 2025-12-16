<script>
import Dialog from 'primevue/dialog';
import InputText from 'primevue/inputtext';
import Button from 'primevue/button';

export default {
  name: 'OrganizationsView',
  components: {
    Dialog,
    InputText,
    Button
  },
  data() {
    return {
      // Видимость диалогового окна
      visible: false,
      // Название новой организации
      newOrgName: '',
      
      // Список организаций
      organizations: [
        {
          id: 1,
          name: 'ООО "Сетевая Безопасность"',
          createdAt: '2023-05-15',
          address: 'г. Москва, ул. Тверская, д. 10, офис 505',
          status: 'active'
        }
      ]
    }
  },
  methods: {
    createOrganization() {
      if (!this.newOrgName) return;

      const newOrg = {
        id: Date.now(),
        name: this.newOrgName,
        createdAt: new Date().toISOString(),
        // Копирование остальных полей
        address: 'г. Москва, ул. Тверская, д. 10, офис 505',
        status: 'active'
      };

      this.organizations.push(newOrg);
      // Сброс данных
      this.newOrgName = '';
      this.visible = false;
    },
    formatDate(dateString) {
      const date = new Date(dateString)
      return date.toLocaleDateString('ru-RU', {
        day: 'numeric',
        month: 'long',
        year: 'numeric'
      })
    }
  }
}
</script>

<template>

  <!-- Кнопка для добавления организации -->
  <div class="flex justify-content-end">
    <button 
      @click="visible = true" 
      class="pi pi-plus p-2 border-round-xl cursor-pointer bg-white border-none shadow-1 text-900"
      title="Добавить"
    ></button>
  </div>

  <!-- Диалоговое окно для создания организации -->
  <Dialog 
    v-model:visible="visible" 
    modal 
    header="Введите имя" 
    :style="{ width: '20rem' }"
  >
    <div class="flex flex-column gap-3">
      <InputText v-model="newOrgName" placeholder="Название организации" class="w-full" />
      <div class="flex justify-content-end">
         <Button label="Создать" @click="createOrganization" />
      </div>
    </div>
  </Dialog>

  <div 
    v-for="organization in organizations" 
    :key="organization.id" 
    class="flex flex-row glass-effect p-4 border-round-xl mt-2"
  >
    <img
        alt="organization logo"
        class="w-3 mr-4 border-round"
        src="https://primefaces.org/cdn/primevue/images/usercard.png"
    />

    <!-- Информация справа -->
    <div class="flex-1">
      <!-- Заголовок и статус -->
      <div class="flex justify-content-between align-items-start mb-3">
        <div>
          <h3 class="text-xl font-bold m-0">{{ organization.name }}</h3>
          <div class="flex align-items-center mt-1">
            <i class="pi pi-calendar mr-2 text-sm"></i>
            <span>Создана: {{ formatDate(organization.createdAt) }}</span>
          </div>
        </div>
        <div class="flex align-items-center">
          <i class="pi pi-circle-fill mr-2 text-green-400"></i>
          <span class="text-sm">Активна </span>
        </div>
      </div>

      <!-- Адрес -->
      <div class="flex align-items-start mb-4">
        <i class="pi pi-map-marker text-500 mr-2 mt-1"></i>
        <div>
          <div class="text-500 text-sm mb-1">Адрес:</div>
          <div class="text-900">{{ organization.address }}</div>
        </div>
      </div>

      <!-- Кнопки действий -->
      <div class="flex gap-2 ">
        <button class="p-2 border-round">
          <i class="pi pi-eye mr-2"></i>
          <span>Просмотр</span>
        </button>
        <button class="p-2 border-round">
          <i class="pi pi-cog mr-2"></i>
          <span>Настройки</span>
        </button>
        <button class="p-2 border-round">
          <i class="pi pi-chart-bar mr-2"></i>
          <span>Аналитика</span>
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>