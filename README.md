# -import json

def load_questions(path='questions.json'):
    with open(path, encoding='utf-8') as f:
        return json.load(f)

def run_quiz(questions):
    score = 0
    for idx, q in enumerate(questions, start=1):
        print(f"\nВопрос {idx}: {q['question']}")
        for i, opt in enumerate(q['options']):
            print(f"  {i}. {opt}")
        try:
            answer = int(input("Ваш ответ (номер варианта): ").strip())
        except ValueError:
            print("Неверный ввод, считаем ответ неверным.")
            continue

        if answer == q['answer']:
            print("Верно!")
            score += 1
        else:
            correct = q['options'][q['answer']]
            print(f"Неверно. Правильный ответ: {correct}")

    print("\n=== Результат ===")
    print(f"Вы ответили верно на {score} из {len(questions)}")

if __name__ == "__main__":
    qs = load_questions()
    run_quiz(qs)
