<script setup>
import { ref } from "vue";

const emits = defineEmits();
const props = defineProps(["isOpen"]);
const dataForm = ref({
    name: "",
    time: "",
});
const addData = () => {
    if (dataForm.value.name === "" && dataForm.value.time === "") {
        alert("Please fill in both name and time fields");
        return;
    }
    const newData = { ...dataForm.value };
    emits("addDataToList", newData);
    dataForm.value.name = "";
    dataForm.value.time = "";
    emits("closeModal", false);
};
const closeModal = () => {
    emits("closeModal", false);
};
</script>

<template>
    <div id="modal"
        class="fixed inset-0 bg-gray-500 bg-opacity-75 flex items-center justify-center transition-all duration-200 ease-in"
        :class="props.isOpen ? 'opacity-100 visible' : 'opacity-0 invisible'">
        <!-- Modal content -->
        <div class="bg-white p-10 rounded shadow-lg w-2/5">
            <div class="mb-6 flex justify-between items-center">
                <h1 class="text-3xl text-gray-800 font-bold">Create data</h1>
                <button @click="closeModal"
                    class="text-base text-white font-medium bg-red-600 w-8 h-8 rounded-full flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-5 h-5">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
            <form class="w-full">
                <div class="flex flex-wrap -mx-3 mb-6">
                    <div class="w-full px-3 mb-6 md:mb-0">
                        <label class="block uppercase tracking-wide text-gray-700 text-xs font-semibold mb-2"
                            for="grid-first-name">
                            Name
                        </label>
                        <input
                            class="appearance-none block w-full text-gray-700 border border-gray-300 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
                            id="grid-first-name" type="text" placeholder="Enter task name " v-model="dataForm.name" />
                    </div>
                    <div class="w-full px-3 mb-6 md:mb-0">
                        <label class="block uppercase tracking-wide text-gray-700 text-xs font-semibold mb-2"
                            for="grid-first-name">
                            Time
                        </label>
                        <input
                            class="appearance-none block w-full text-gray-700 border border-gray-300 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
                            id="grid-first-name" type="number" placeholder="Enter time" v-model="dataForm.time" />
                    </div>
                </div>

                <button class="text-base text-white font-medium px-5 py-3 bg-gray-900 rounded-lg" @click.prevent="addData">
                    Submit
                </button>
            </form>
        </div>
    </div>
</template>

<style scoped></style>
