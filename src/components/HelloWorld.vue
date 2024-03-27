<script setup>
import { ref } from "vue";

const side1 = ref(0);
const side2 = ref(0);
const side3 = ref(0);
const result = ref("");

const analyzeTriangle = () => {
    const a = parseFloat(side1.value);
    const b = parseFloat(side2.value);
    const c = parseFloat(side3.value);

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
    <div class="flex w-screen h-screen justify-center items-center text-black">
        <div class="bg-white p-12 rounded-3xl flex flex-col w-fit shadow-xl">
            <div class="font-bold text-2xl mb-8">Enter the length of sides</div>
            <div class="m-2 flex">
                <p class="w-12 font-semibold">Side 1</p>
                <input
                    @focus="$event.target.select()"
                    @keyup.enter="analyzeTriangle"
                    type="number"
                    min="0"
                    v-model.number="side1"
                    class="bg-white border-[0.1rem] border-black rounded-lg ml-4 text-center"
                />
            </div>
            <div class="m-2 flex">
                <p class="w-12 font-semibold">Side 2</p>
                <input
                    @focus="$event.target.select()"
                    @keyup.enter="analyzeTriangle"
                    type="number"
                    min="0"
                    v-model.number="side2"
                    class="bg-white border-[0.1rem] border-black rounded-lg ml-4 text-center"
                />
            </div>
            <div class="m-2 flex">
                <p class="w-12 font-semibold">Side 3</p>
                <input
                    @focus="$event.target.select()"
                    @keyup.enter="analyzeTriangle"
                    type="number"
                    min="0"
                    v-model.number="side3"
                    class="bg-white border-[0.1rem] border-black rounded-lg ml-4 text-center"
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
    </div>
</template>

<style scoped></style>

