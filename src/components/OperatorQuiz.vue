<template>
    <div>
        <div v-if="isQuizStarted">
            <h4>{{ operandLeft }} {{ operator }} {{ operandRight }}</h4>
            <button @click="selectAnswer(answer)" v-for="(answer, index) of answers" :key="index">{{ answer }}</button>
        </div>
        <div v-if="!isQuizStarted">
            <button @click="startQuiz">Start</button>
        </div>
        <button @click="$emit('onBack')">Back</button>
    </div>
</template>

<script>
export default {
    props: ["operator"],
    data() {
        return {
            isQuizStarted: false,
            operandLeft: null,
            operandRight: null,
            answers: [],
            expectedAnswer: null
        }
    },
    methods: {
        selectAnswer(answerSelected) {
            if (answerSelected !== this.expectedAnswer) {
                alert('WRONG ANSWER!!');
            }
            this.startQuiz();
        },
        startQuiz() {
            this.isQuizStarted = true;
            this.operandLeft = parseInt(Math.random() * 13);
            this.operandRight = parseInt(Math.random() * 13);

            const methods = {
                '+': (a, b) => a + b,
                '-': (a, b) => a - b,
                '/': (a, b) => a / b,
                '*': (a, b) => a * b,
            };

            const methodToUse = methods[this.operator];
            this.expectedAnswer = methodToUse(this.operandLeft, this.operandRight);
            this.answers = [this.expectedAnswer];

            // Add 4 more unique random answers
            while (this.answers.length < 5) {
                const randomAnswer = methodToUse(
                    parseInt(Math.random() * 13),
                    parseInt(Math.random() * 13)
                );

                if (!this.answers.includes(randomAnswer)) {
                    this.answers.push(randomAnswer);
                }
            }

            // Shuffle the array so the correct answer isn't always first
            this.answers.sort(() => Math.random() - 0.5);
        }
    }
}
</script>

<style scoped></style>