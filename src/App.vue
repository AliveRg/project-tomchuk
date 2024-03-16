<script setup></script>

<template>
  <h1>Тест по выбору профессии</h1>

  <div class="ident" v-if="currentQuestion">
    <h2>{{ currentQuestion.text }}</h2>
    <div
      style="display: flex; align-items: start"
      v-for="option in currentQuestion.options"
      :key="option.value"
    >
      <input
        style="margin-top: 5px"
        type="radio"
        :id="option.value"
        :value="option.value"
        v-model="selectedOption"
      />
      <label :for="option.value">{{ option.label }}</label>
    </div>
    <button @click="nextQuestion">Next</button>
  </div>
  <div v-else>
    <h2>Thank you for completing the questionnaire!</h2>
    <p>Your result: {{ result }}</p>
  </div>
</template>

<script lang="js">
export default {
  data() {
    return {
      // Массив объектов с вопросами и вариантами ответов
      questions: [
        {
          name: 'q1',
          text: '1. Какая часть урока вам больше всего запоминается?',
          options: [
            {
              value: 'a',
              label: 'a) Моменты, связанные с решением задач и выполнением практических упражнений.'
            },
            {
              value: 'b',
              label: 'b) Интересные факты и информация, которую вы узнали на лекциях.'
            },
            { value: 'c', label: 'c) Обсуждения и обмен мнениями с другими учениками.' },
            {
              value: 'd',
              label: 'd) Моменты, когда можно было отдохнуть или немного расслабиться.'
            }
          ]
        },
        {
          name: 'q2',
          text: '2. Как вы предпочитаете проводить свободное время вне уроков?',
          options: [
            { value: 'a', label: 'a) Занятия спортом или активные игры на свежем воздухе.' },
            { value: 'b', label: 'b) Чтение книг или просмотр фильмов, которые вас интересуют.' },
            { value: 'c', label: 'c) Встречи с друзьями и участие в различных мероприятиях.' },
            {
              value: 'd',
              label: 'd) Время в одиночестве, чтобы делать что-то привычное и монотонное.'
            }
          ]
        },
        {
          name: 'q3',
          text: '3. Как вы обычно принимаете решения?',
          options: [
            { value: 'a', label: 'a) Анализируя информацию и взвешивая все варианты.' },
            { value: 'b', label: 'b) Слушая свое воображение и исследуя новые возможности.' },
            { value: 'c', label: 'c) Обсуждая с другими и получая их мнение.' },
            { value: 'd', label: 'd) Следуя инструкциям и рутинным шагам.' }
          ]
        },
        {
          name: 'q4',
          text: '4. Что для вас является наиболее важным в работе?',
          options: [
            { value: 'a', label: 'a) Завершение задач и достижение конкретных результатов.' },
            { value: 'b', label: 'b) Возможность проявить себя и воплотить свои идеи.' },
            { value: 'c', label: 'c) Взаимодействие с коллегами и общение с клиентами.' },
            { value: 'd', label: 'd) Постоянство и стабильность в рутинной работе.' }
          ]
        },
        {
          name: 'q5',
          text: '5. Как вы предпочитаете организовывать свое рабочее пространство?',
          options: [
            { value: 'a', label: 'a) Упорядоченные и аккуратные рабочие области.' },
            { value: 'b', label: 'b) Вдохновляющие и необычные рабочие пространства.' },
            { value: 'c', label: 'c) Общие рабочие зоны и коллективное творчество.' },
            { value: 'd', label: 'd) Простые и функциональные рабочие условия без лишних деталей.' }
          ]
        },
        {
          name: 'q6',
          text: '6. Какие аспекты карьеры для вас наиболее важны?',
          options: [
            { value: 'a', label: 'a) Профессиональный рост и развитие навыков.' },
            { value: 'b', label: 'b) Возможность влиять на окружающий мир и вносить изменения.' },
            { value: 'c', label: 'c) Баланс между работой и личной жизнью.' },
            { value: 'd', label: 'd) Стабильность и регулярный доход.' }
          ]
        },
        {
          name: 'q7',
          text: '7. Что вас больше всего вдохновляет?',
          options: [
            { value: 'a', label: 'a) Успехи и достижения других людей.' },
            { value: 'b', label: 'b) Новые идеи и творческие возможности.' },
            { value: 'c', label: 'c) Совместная работа и достижение общих целей.' },
            { value: 'd', label: 'd) Мирные и спокойные моменты без лишней активности.' }
          ]
        },
        {
          name: 'q8',
          text: '8. Что вам больше нравится делать в свободное время?',
          options: [
            { value: 'a', label: 'a) Заниматься рукоделием или другими творческими хобби.' },
            { value: 'b', label: 'b) Путешествовать и открывать новые места.' },
            { value: 'c', label: 'c) Проводить время с животными или заботиться о растениях.' },
            { value: 'd', label: 'd) Отдыхать и расслабляться, ничего не делая.' }
          ]
        },
        {
          name: 'q9',
          text: '9. Как вы относитесь к изменениям и неожиданностям?',
          options: [
            { value: 'a', label: 'a) Предпочитаю избегать изменений и придерживаться привычного.' },
            { value: 'b', label: 'b) Люблю новые вызовы и готов принимать перемены.' },
            {
              value: 'c',
              label: 'c) Могу адаптироваться к изменениям в зависимости от обстоятельств.'
            },
            { value: 'd', label: 'd) Чувствую себя неуютно, когда что-то меняется внезапно.' }
          ]
        },

        {
          name: 'q10',
          text: '10. Как вы относитесь к работе в команде?',
          options: [
            {
              value: 'a',
              label: 'a) Предпочитаю работать самостоятельно, чтобы не зависеть от других.'
            },
            { value: 'b', label: 'b) Люблю сотрудничать с другими, чтобы достигать общих целей.' },
            {
              value: 'c',
              label:
                'c) Могу работать как в команде, так и самостоятельно, в зависимости от ситуации.'
            },
            {
              value: 'd',
              label:
                'd) Не чувствую себя комфортно в коллективе и предпочитаю избегать групповых проектов.'
            }
          ]
        },
        {
          name: 'q11',
          text: '11. Что для вас важнее: процесс или результат?',
          options: [
            {
              value: 'a',
              label: 'a) Главное для меня – сам процесс работы, а не итоговый результат.'
            },
            {
              value: 'b',
              label:
                'b) Для меня важнее получить конечный результат, даже если процесс не всегда интересен.'
            },
            { value: 'c', label: 'c) Я стараюсь найти баланс между процессом и результатом.' },
            {
              value: 'd',
              label:
                'd) Мне важно, чтобы процесс работы был интересным, но и результат играет большую роль.'
            }
          ]
        },
        {
          name: 'q12',
          text: '12. Как вы относитесь к рутинным задачам?',
          options: [
            {
              value: 'a',
              label: 'a) Чувствую себя неуютно, когда приходится выполнять монотонные задания.'
            },
            {
              value: 'b',
              label:
                'b) Не против выполнять рутинные задачи, если это необходимо для достижения цели.'
            },
            {
              value: 'c',
              label:
                'c) Могу эффективно выполнять рутинные задания, если они входят в мои обязанности.'
            },
            {
              value: 'd',
              label:
                'd) Мне нравится выполнять рутинные задачи, это помогает мне сосредоточиться и успокоиться.'
            }
          ]
        }
        // Добавьте сюда остальные вопросы в таком же формате
      ],
      // Массив для хранения ответов пользователя
      currentQuestionIndex: 0,
      selectedOption: null,
      result: null
    }
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentQuestionIndex]
    }
  },
  methods: {
    nextQuestion() {
      if (this.selectedOption !== null) {
        if (this.currentQuestionIndex < this.questions.length - 1) {
          this.currentQuestionIndex++
          this.selectedOption = null
        } else {
          this.calculateResult()
        }
      }
    },
    // Метод для подсчета результатов
    calculateResults() {
      // Подсчитываем количество ответов каждого типа
      const counts = { a: 0, b: 0, c: 0, d: 0 }
      this.answers.forEach((answer) => {
        counts[answer]++
      })
      // Определяем тип с максимальным количеством ответов
      const maxCount = Math.max(...Object.values(counts))
      let result = ''
      // Выводим результат в зависимости от наибольшего количества ответов
      if (maxCount === counts.a) {
        result =
          'Тип "a": Это может указывать на предпочтение творческих и нестандартных видов работы, где требуется оригинальный подход и готовность к постоянным изменениям.'
      } else if (maxCount === counts.b) {
        result =
          'Тип "b": Это может свидетельствовать о склонности к аналитическому мышлению, структурированию и выполнению конкретных задач, где требуется логика и системность.'
      } else if (maxCount === counts.c) {
        result =
          'Тип "c": Это указывает на интерес к взаимодействию с людьми, работе в коллективе и умению общаться, что может подталкивать к выбору профессии, связанной с социальными аспектами и межличностными отношениями.'
      } else if (maxCount === counts.d) {
        result =
          'Тип "d": Это может свидетельствовать о склонности к монотонным видам работы, где требуется выполнение рутинных задач и усидчивость.'
      }
      // Устанавливаем результат
      this.result = result
    }
  }
}
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f3f5f7;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

#app {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 30px;
  max-width: 600px;
  min-height: 600px;
  width: 100%;
}

h2 {
  margin-top: 0;
}

.question {
  margin-bottom: 20px;
}
.ident {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

input[type='radio'] {
  display: none;
}

label {
  display: block;
  position: relative;
  padding-left: 30px;
  margin-bottom: 10px;
  cursor: pointer;
  font-size: 16px;
  line-height: 1.5;
}

label:before {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 20px;
  height: 20px;
  border: 2px solid #007bff;
  border-radius: 50%;
  transition: border-color 0.3s;
}

input[type='radio']:checked + label:before {
  background-color: #007bff;
  border-color: #007bff;
}

button {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #0056b3;
}
</style>
