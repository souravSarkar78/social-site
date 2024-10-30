<template>
  <div class="relative">
    <button 
      @click="isOpen = !isOpen"
      class="relative p-2 rounded-full hover:bg-gray-100 dark:hover:bg-gray-700 transition"
    >
      <svg class="w-6 h-6 text-gray-600 dark:text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
      </svg>
      <div v-if="unreadCount > 0" class="absolute top-0 right-0 w-4 h-4 bg-red-500 rounded-full flex items-center justify-center">
        <span class="text-xs text-white">{{ unreadCount }}</span>
      </div>
    </button>

    <div 
      v-if="isOpen"
      class="absolute right-0 mt-2 w-80 bg-white dark:bg-gray-800 rounded-lg shadow-lg overflow-hidden z-50"
    >
      <div class="p-4 border-b border-gray-200 dark:border-gray-700">
        <div class="flex items-center justify-between">
          <h3 class="text-lg font-semibold">Notifications</h3>
          <button 
            v-if="hasUnread"
            @click="markAllAsRead"
            class="text-sm text-indigo-600 hover:text-indigo-800 dark:text-indigo-400 dark:hover:text-indigo-300"
          >
            Mark all as read
          </button>
        </div>
      </div>

      <div class="divide-y divide-gray-200 dark:divide-gray-700 max-h-[400px] overflow-y-auto">
        <div
          v-for="notification in notifications.slice(0, 5)"
          :key="notification.id"
          :class="[
            'p-4 hover:bg-gray-50 dark:hover:bg-gray-700/50 transition cursor-pointer',
            { 'bg-indigo-50 dark:bg-indigo-900/20': !notification.read }
          ]"
          @click="handleNotificationClick(notification)"
        >
          <div class="flex items-start space-x-3">
            <div class="flex-shrink-0">
              <component 
                :is="notificationIcons[notification.type]" 
                class="w-6 h-6"
                :class="notificationColors[notification.type]"
              />
            </div>
            <div class="flex-1 min-w-0">
              <p class="text-sm font-medium text-gray-900 dark:text-gray-100">
                {{ notification.title }}
              </p>
              <p class="text-sm text-gray-600 dark:text-gray-400">
                {{ notification.message }}
              </p>
              <p class="text-xs text-gray-500 dark:text-gray-500 mt-1">
                {{ formatTime(notification.timestamp) }}
              </p>
            </div>
            <div v-if="!notification.read" class="flex-shrink-0">
              <div class="w-2 h-2 bg-indigo-600 rounded-full"></div>
            </div>
          </div>
        </div>
      </div>

      <div v-if="notifications.length === 0" class="p-4 text-center text-gray-500 dark:text-gray-400">
        No notifications
      </div>

      <div class="p-4 border-t border-gray-200 dark:border-gray-700">
        <NuxtLink 
          to="/notifications"
          @click="isOpen = false"
          class="block w-full text-center text-sm text-indigo-600 hover:text-indigo-800 dark:text-indigo-400 dark:hover:text-indigo-300"
        >
          View all notifications
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
const isOpen = ref(false)
const notifications = ref([
  {
    id: 1,
    type: 'mention',
    title: 'New Mention',
    message: '@janedoe mentioned you in a comment',
    timestamp: Date.now() - 1000 * 60 * 5,
    read: false
  },
  {
    id: 2,
    type: 'like',
    title: 'New Like',
    message: 'Your story "The Last Chapter" received a like',
    timestamp: Date.now() - 1000 * 60 * 30,
    read: false
  },
  {
    id: 3,
    type: 'comment',
    title: 'New Comment',
    message: 'Someone commented on your poem',
    timestamp: Date.now() - 1000 * 60 * 60 * 2,
    read: true
  }
])

// ... rest of the existing code remains the same ...
</script>