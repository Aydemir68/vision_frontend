<script>
export default {
  name: 'OrganizationCard',
  props: {
    organization: {
      type: Object,
      default: () => ({
        name: 'ООО "Сетевая Безопасность"',
        createdAt: '2023-05-15',
        address: 'г. Москва, ул. Тверская, д. 10, офис 505',
        status: 'active'
      })
    }
  },
  computed: {
    formattedDate() {
      const date = new Date(this.organization.createdAt)
      return date.toLocaleDateString('ru-RU', {
        day: 'numeric',
        month: 'long',
        year: 'numeric'
      })
    },
  }
}
</script>

<template>
  <div class="flex flex-row glass-effect p-4 border-round-xl">
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
            <span>Создана: {{ formattedDate }}</span>
          </div>
        </div>
        <div class="flex align-items-center">
          <i class="pi pi-circle-fill mr-2"></i>
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
      <div class="flex gap-2">
        <button class="p-button p-button-sm p-button-outlined">
          <i class="pi pi-eye mr-2"></i>
          <span>Просмотр</span>
        </button>
        <button class="p-button p-button-sm p-button-outlined">
          <i class="pi pi-cog mr-2"></i>
          <span>Настройки</span>
        </button>
        <button class="p-button p-button-sm p-button-outlined">
          <i class="pi pi-chart-bar mr-2"></i>
          <span>Аналитика</span>
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>