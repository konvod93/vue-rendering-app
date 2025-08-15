<template>
  <section class="section">
    <h2>📋 Управление пользователями</h2>
    <div class="controls">
      <button @click="showUsers = !showUsers">
        {{ showUsers ? '🙈 Скрыть пользователей' : '👀 Показать пользователей' }}
      </button>
      <button v-if="showUsers" @click="showOnlyActive = !showOnlyActive">
        {{ showOnlyActive ? '👥 Показать всех' : '✅ Только активные' }}
      </button>
    </div>

    <div v-if="showUsers">
      <div class="stats">
        <div class="stat-item">
          <div class="stat-number">{{ totalUsers }}</div>
          <div>Всего пользователей</div>
        </div>
        <div class="stat-item">
          <div class="stat-number">{{ activeUsers }}</div>
          <div>Активных</div>
        </div>
        <div class="stat-item">
          <div class="stat-number">{{ displayedUsers.length }}</div>
          <div>Показано</div>
        </div>
      </div>

      <div class="controls">
        <input v-model="newUser.name" placeholder="Имя пользователя" @keyup.enter="addUser" />
        <input v-model="newUser.email" placeholder="Email" @keyup.enter="addUser" />
        <select v-model="newUser.status">
          <option value="active">Активный</option>
          <option value="inactive">Неактивный</option>
        </select>
        <button @click="addUser">➕ Добавить</button>
      </div>

      <div v-if="displayedUsers.length === 0" class="empty-state">
        <h3>🤷‍♂️ Пользователи не найдены</h3>
        <p v-if="showOnlyActive">Попробуйте показать всех пользователей</p>
        <p v-else>Добавьте первого пользователя!</p>
      </div>

      <div v-else class="user-list">
        <div v-for="user in displayedUsers" :key="user.id" class="user-card">
          <div class="user-name">{{ user.name }}</div>
          <div class="user-email">📧 {{ user.email }}</div>
          <div class="controls" style="margin-top: 10px;">
            <span :class="['user-status', user.status === 'active' ? 'status-active' : 'status-inactive']">
              {{ user.status === 'active' ? '✅ Активный' : '❌ Неактивный' }}
            </span>
            <button @click="toggleUserStatus(user)">
              {{ user.status === 'active' ? '🔒 Деактивировать' : '🔓 Активировать' }}
            </button>
            <button @click="removeUser(user.id)" style="background: #e74c3c;">
              🗑️ Удалить
            </button>
          </div>
        </div>
      </div>
    </div>

    <div v-else class="empty-state">
      <h3>👆 Нажмите кнопку выше, чтобы увидеть список пользователей</h3>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

const showUsers = ref(false)
const showOnlyActive = ref(false)
const nextId = ref(4)
const newUser = ref({ name: '', email: '', status: 'active' })

const users = ref([
  { id: 1, name: 'Анна Иванова', email: 'anna@example.com', status: 'active' },
  { id: 2, name: 'Петр Петров', email: 'petr@example.com', status: 'inactive' },
  { id: 3, name: 'Мария Сидорова', email: 'maria@example.com', status: 'active' }
])

const displayedUsers = computed(() =>
  showOnlyActive.value ? users.value.filter(u => u.status === 'active') : users.value
)
const totalUsers = computed(() => users.value.length)
const activeUsers = computed(() => users.value.filter(u => u.status === 'active').length)

function addUser() {
  if (newUser.value.name.trim() && newUser.value.email.trim()) {
    users.value.push({
      id: nextId.value++,
      name: newUser.value.name.trim(),
      email: newUser.value.email.trim(),
      status: newUser.value.status
    })
    newUser.value.name = ''
    newUser.value.email = ''
    newUser.value.status = 'active'
  }
}

function removeUser(id) {
  users.value = users.value.filter(u => u.id !== id)
}

function toggleUserStatus(user) {
  user.status = user.status === 'active' ? 'inactive' : 'active'
}
</script>

<style scoped>
/* можно перенести стили из index.html сюда */
</style>