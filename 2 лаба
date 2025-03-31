#include <stdio.h>
#include <stdlib.h>
#include <locale.h>

// Функция для вычисления среднего арифметического чисел в файле
double calculate_average(FILE* file, int total_elements) {
    int sum = 0;

    rewind(file); // Переход в начало файла
    for (int i = 0; i < total_elements; i++) {
        int num;
        fscanf_s(file, "%d", &num);
        sum += num; // Суммируем числа
    }

    return (double)sum / total_elements; // Вычисляем среднее арифметическое
}

// Функция для обмена двух элементов в текстовом файле
void swap_elements(FILE* file, int pos1, int pos2, int total_elements) {
    int numbers[total_elements];

    // Чтение всех чисел из файла в массив
    rewind(file);
    for (int i = 0; i < total_elements; i++) {
        fscanf_s(file, "%d", &numbers[i]);
    }

    // Обмен значениями
    int temp = numbers[pos1];
    numbers[pos1] = numbers[pos2];
    numbers[pos2] = temp;

    // Запись изменённого массива обратно в файл
    freopen(NULL, "w", file);
    for (int i = 0; i < total_elements; i++) {
        fprintf(file, "%d\n", numbers[i]);
    }
}

// Функция для обмена первого и последнего числа в файле
void swap_first_and_last(FILE* file, int total_elements) {
    if (total_elements < 2) {
        printf("В файле недостаточно чисел для обмена.\n");
        return;
    }

    int numbers[total_elements];

    // Чтение всех чисел из файла в массив
    rewind(file);
    for (int i = 0; i < total_elements; i++) {
        fscanf_s(file, "%d", &numbers[i]);
    }

    // Обмен первого и последнего элемента
    int temp = numbers[0];
    numbers[0] = numbers[total_elements - 1];
    numbers[total_elements - 1] = temp;

    // Запись изменённого массива обратно в файл
    freopen(NULL, "w", file);
    for (int i = 0; i < total_elements; i++) {
        fprintf(file, "%d\n", numbers[i]);
    }
}

// Главная функция программы
int main(int argc, char* argv[]) {
    setlocale(LC_ALL, "rus"); // Установка локали для поддержки русского языка

    // Проверка наличия имени файла
    if (argc < 2) {
        printf("Укажите имя файла как первый аргумент командной строки.\n");
        return 1;
    }

    // Открытие файла
    FILE* file;
    fopen_s(&file, argv[1], "w+");
    if (!file) {
        printf("Не удалось открыть файл.\n");
        return 1;
    }

    // Ввод количества чисел
    printf("Введите количество чисел: ");
    int n;
    scanf_s("%d", &n);

    // Ввод чисел с клавиатуры и запись в файл
    printf("Введите числа:\n");
    for (int i = 0; i < n; i++) {
        int num;
        scanf_s("%d", &num);
        fprintf(file, "%d\n", num);
    }

    // Чтение и вывод чисел из файла
    printf("Содержимое файла:\n");
    rewind(file);
    for (int i = 0; i < n; i++) {
        int num;
        fscanf_s(file, "%d", &num);
        printf("%d ", num);
    }
    printf("\n");

    // Вычисление среднего арифметического
    double average = calculate_average(file, n);
    printf("Среднее арифметическое всех чисел: %.2f\n", average);

    // Обмен первого и последнего числа
    swap_first_and_last(file, n);
    printf("Содержимое файла после обмена первого и последнего числа:\n");
    rewind(file);
    for (int i = 0; i < n; i++) {
        int num;
        fscanf_s(file, "%d", &num);
        printf("%d ", num);
    }
    printf("\n");

    // Обмен элементов по указанным позициям
    printf("Введите позиции для обмена (от 0 до %d):\n", n - 1);
    int pos1, pos2;
    scanf_s("%d %d", &pos1, &pos2);

    // Проверка корректности введённых позиций
    if (pos1 < 0 || pos1 >= n || pos2 < 0 || pos2 >= n) {
        printf("Некорректные позиции.\n");
    } else {
        swap_elements(file, pos1, pos2, n);

        // Вывод после обмена
        printf("Содержимое файла после обмена элементов:\n");
        rewind(file);
        for (int i = 0; i < n; i++) {
            int num;
            fscanf_s(file, "%d", &num);
            printf("%d ", num);
        }
        printf("\n");
    }

    fclose(file); // Закрытие файла
    return 0;
}
