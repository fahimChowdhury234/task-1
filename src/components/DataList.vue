<script setup>
import { computed } from "vue";

const props = defineProps(["dataList", "isOpen"]);
const emits = defineEmits();

const openModal = () => {
    emits("openModal", true);
};
const removeData = (e) => {
    emits("removeData", e);
};
const hasData = computed(() => props.dataList.length > 0);
</script>

<template>
    <div class="w-3/4 mx-auto">
        <div class="my-10 flex justify-between items-center">
            <h1 class="text-5xl text-gray-700 font-bold">Data list</h1>
            <button class="text-base text-white font-medium px-5 py-3 bg-gray-900 rounded-lg flex items-center gap-2"
                @click="openModal">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="w-6 h-6">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
                </svg>

                Add data
            </button>
        </div>
        <table class="min-w-full divide-y divide-gray-200 border border-gray-300" v-if="hasData">
            <thead>
                <tr>
                    <th
                        class="px-6 py-3 text-center bg-gray-50 text-sm leading-4 font-medium text-gray-500 uppercase tracking-wider border-r border-gray-300">
                        Id
                    </th>
                    <th
                        class="px-6 py-3 bg-gray-50 text-center text-sm leading-4 font-medium text-gray-500 uppercase tracking-wider border-r border-gray-300">
                        Name
                    </th>
                    <th
                        class="px-6 py-3 bg-gray-50 text-center text-sm leading-4 font-medium text-gray-500 uppercase tracking-wider border-r border-gray-300">
                        Time
                    </th>
                    <th
                        class="px-6 py-3 bg-gray-50 text-center text-sm leading-4 font-medium text-gray-500 uppercase tracking-wider">
                        Action
                    </th>
                </tr>
            </thead>
            <tbody class="bg-white">
                <tr v-for="(data, i) in props.dataList" :key="i" class="border-b border-gray-300">
                    <td class="px-6 py-4 border-r border-gray-300 text-center">
                        {{ i }}
                    </td>
                    <td class="px-6 py-4 border-r border-gray-300 text-center">
                        {{ data.name }}
                    </td>
                    <td class="px-6 py-4 border-r border-gray-300 text-center">
                        {{ data.time }} minutes
                    </td>
                    <td class="px-6 py-4 text-center">
                        <button
                            class="px-4 py-2 border font-medium  border-red-600 text-red-600 rounded-lg transition-all duration-200 ease-in hover:bg-red-100"
                            @click="removeData(i)">
                            Delete
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>
        <div v-else class="flex justify-center gap-4 flex-col items-center text-red-600">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
                class="w-14 h-14">
                <path stroke-linecap="round" stroke-linejoin="round"
                    d="M12 9v3.75m-9.303 3.376c-.866 1.5.217 3.374 1.948 3.374h14.71c1.73 0 2.813-1.874 1.948-3.374L13.949 3.378c-.866-1.5-3.032-1.5-3.898 0L2.697 16.126ZM12 15.75h.007v.008H12v-.008Z" />
            </svg>

            <h2 class="text-3xl  font-semibold text-center ">No data found. <br> Please add some data</h2>
        </div>
    </div>
</template>

<style scoped></style>
