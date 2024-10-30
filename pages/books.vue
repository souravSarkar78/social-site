<template>
  <div class="container mx-auto px-4 py-8">
    <div class="grid grid-cols-1 md:grid-cols-12 gap-6">
      <div class="md:col-span-3">
        <SideBar />
      </div>
      <main class="md:col-span-9">
        <h1 class="text-2xl font-bold mb-6">My Books</h1>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div v-for="i in 6" :key="i" class="bg-white dark:bg-gray-800 rounded-lg shadow overflow-hidden">
            <img src="https://via.placeholder.com/400x250" alt="Book Cover" class="w-full h-48 object-cover">
            <div class="p-4">
              <h3 class="text-lg font-semibold mb-2">Book Title {{ i }}</h3>
              <p class="text-sm text-gray-600 dark:text-gray-400 mb-4">A brief description of the book goes here...</p>
              <div class="flex justify-between items-center">
                <span class="text-sm text-gray-500">Published: Jan 2024</span>
                <button class="text-indigo-600 hover:text-indigo-800">Edit</button>
              </div>
            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>