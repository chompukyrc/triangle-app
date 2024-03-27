<script setup>
import { ref } from "vue";

const side1 = ref(0);
const side2 = ref(0);
const side3 = ref(0);
const result = ref("");

const analyzeTriangle = () => {
    if (isNaN(side1.value) || side1.value === "") {
        alert("Side 1 is not a number");
        return;
    } else if (isNaN(side2.value) || side2.value === "") {
        alert("Side 2 is not a number");
        return;
    } else if (isNaN(side3.value) || side3.value === "") {
        alert("Side 3 is not a number");
        return;
    }

    const a = parseFloat(side1.value);
    const b = parseFloat(side2.value);
    const c = parseFloat(side3.value);

    // Check for a valid triangle first
    if (a + b <= c || a + c <= b || b + c <= a) {
        result.value = "Not a valid triangle";
        return;
    }

    // Check for a valid triangle first
    if (a + b <= c || a + c <= b || b + c <= a) {
        result.value = "Not a valid triangle";
        return;
    }

    // Calculate the angles in degrees
    const angleA =
        Math.acos((b * b + c * c - a * a) / (2 * b * c)) * (180 / Math.PI);
    const angleB =
        Math.acos((a * a + c * c - b * b) / (2 * a * c)) * (180 / Math.PI);
    const angleC =
        Math.acos((a * a + b * b - c * c) / (2 * a * b)) * (180 / Math.PI);

    // Round the angles to avoid floating point precision issues
    const alpha = Math.round(angleA);
    const beta = Math.round(angleB);
    const gamma = Math.round(angleC);

    // Determine the triangle type based on angles
    if (alpha === 60 && beta === 60 && gamma === 60) {
        result.value = "Equilateral triangle";
    } else if (alpha === beta || alpha === gamma || beta === gamma) {
        result.value = "Isosceles triangle";
    } else if (alpha === 90 || beta === 90 || gamma === 90) {
        result.value = "Right triangle";
    } else {
        result.value = "Scalene triangle";
    }
};
</script>

<template>
    <div
        class="flex flex-col w-screen h-screen justify-between items-center text-black font-mono"
    >
        <div></div>
        <div
            class="bg-white p-8 mx-2 rounded-3xl flex flex-col w-fit shadow-xl"
        >
            <div class="font-bold text-2xl mb-8 text-center">
                Enter the length of sides
            </div>
            <div class="m-2 flex">
                <p class="w-24 font-semibold text-center">Side 1</p>
                <input
                    @focus="$event.target.select()"
                    @keyup.enter="analyzeTriangle"
                    type="number"
                    min="0"
                    v-model.number="side1"
                    class="bg-white border-[0.1rem] border-black rounded-lg ml-4 text-center w-full"
                />
            </div>
            <div class="m-2 flex">
                <p class="w-24 font-semibold text-center">Side 2</p>
                <input
                    @focus="$event.target.select()"
                    @keyup.enter="analyzeTriangle"
                    type="number"
                    min="0"
                    v-model.number="side2"
                    class="bg-white border-[0.1rem] border-black rounded-lg ml-4 text-center w-full"
                />
            </div>
            <div class="m-2 flex">
                <p class="w-24 font-semibold text-center">Side 3</p>
                <input
                    @focus="$event.target.select()"
                    @keyup.enter="analyzeTriangle"
                    type="number"
                    min="0"
                    v-model.number="side3"
                    class="bg-white border-[0.1rem] border-black rounded-lg ml-4 text-center w-full"
                />
            </div>
            <button
                @click="analyzeTriangle"
                @keyup.enter="analyzeTriangle"
                class="bg-blue-300 mt-4 m-2 py-1"
            >
                Enter
            </button>
            <div v-if="result" class="mt-4 text-center text-xl font-semibold">
                "{{ result }}"
            </div>
        </div>
        <div class="">
            <a
                href="https://github.com/chompukyrc/triangle-app"
                class="flex items-center justify-center p-2 rounded-md"
                target="_blank"
                rel="noopener noreferrer"
                title="GitHub"
            >
                <svg
                    class="w-8 h-8 text-white"
                    fill="currentColor"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                    aria-hidden="true"
                >
                    <path
                        d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.775.418-1.305.762-1.605-2.666-.3-5.467-1.333-5.467-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.687.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"
                    />
                </svg>
            </a>
            <div
                class="text-white font-mono w-screen flex justify-center mb-1 text-xs text-center"
            >
                Assignment in IT Entrepreneurship And Management 2566
            </div>
            <div
                class="text-white font-mono w-screen flex justify-center pb-2 text-sm"
            >
                <div class="flex items-center">
                    64010037
                    <div
                        class="rounded-full w-1 h-1 bg-white flex items-center justify-center mx-2"
                    ></div>
                    64010232
                    <div
                        class="rounded-full w-1 h-1 bg-white flex items-center justify-center mx-2"
                    ></div>
                    64010443
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped></style>

