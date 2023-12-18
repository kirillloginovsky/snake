#include <iostream>
#include <fstream>
#include <algorithm>
using namespace std;
void swapR(int** array, int row1, int row2, int N) {
    for (int j = 0; j < N; ++j) {
        swap(array[row1][j], array[row2][j]);
    }
}
void swapC(int** arr, int col1, int col2, int N) {
    for (int i = 0; i < N; ++i) {
        // меняю столбцы
        int temp = arr[i][col1];
        arr[i][col1] = arr[i][col2];
        arr[i][col2] = temp;
    }
}

int main() {
    setlocale(LC_ALL, "RU");
    int povtor = 5;
    while (povtor == 5) {
        int N = 0;
        int value = 0;
        cout << "Введите число N: ";
        cin >> N;
        while (cin.fail() == 1) {
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout << "Ошибка. Введите число!" << endl;
            cin >> N;
        }
        while (N <= 0) {
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout << "Ошибка. Число должно быть больше нуля!" << endl;
            cin >> N;
        }
        int** matrix = new int* [N];
        for (int i = 0; i < N; ++i) {
            matrix[i] = new int[N];
        }

        cout << "С какого угла вы хотите начать змейку?" << endl << "Введите соответствующее число: " << endl << "1 - с левого верхнего" << endl << "2 - с левого нижнего" << endl << "3 - с правого верхнего" << endl << "4 - с правого нижнего" << endl;
        cin >> value;
        while (cin.fail() == 1) {
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');  // чистка
            cout << "Ошибка. Введите число!" << endl;
            cin >> value;
        }
        while (value <= 0 && value > 4) {
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout << "Ошибка. Число должно быть больше нуля!" << endl;
            cin >> value;
        }

        int num = 1;
        int num2 = 1;
        int a = 0;
        int b = N - 1;
        int num3 = 1;
        int num4 = N * N;

        switch (value)
        {
        case 1:
            for (int diag = 0; diag < N * 2; ++diag) {
                for (int i = max(0, diag - N + 1); i <= min(diag, N - 1); ++i) {
                    int j = diag - i;
                    if (diag % 2 == 0) {
                        matrix[i][j] = num;
                    }
                    else {
                        matrix[j][i] = num;
                    }
                    ++num;
                }
            }
            // Вывести полученный массив
            cout << "Полученный массив:" << endl;
            for (int i = 0; i < N; ++i) {
                for (int j = 0; j < N; ++j) {
                    cout << matrix[i][j] << '\t';
                }
                cout << endl;
            }
            cout << "Массив успешно сохранен в файл output.txt." << endl;
            break;
        case 2:
            for (int diag = 0; diag < N * 2; ++diag) {
                for (int i = max(0, diag - N + 1); i <= min(diag, N - 1); ++i)
                {
                    int j = diag - i;
                    if (diag % 2 == 0)
                    {
                        matrix[i][j] = num3;
                    }
                    else {
                        matrix[j][i] = num3;
                    }
                    ++num3;
                }
            }
            if (N % 2 == 0)
            {
                for (int i = 0; i < (N / 2); i++) {
                    swapR(matrix, a, b, N);
                    a++;
                    b--;
                }
            }
            else
            {
                for (int i = 0; i < (N - 1) / 2; i++) {
                    swapR(matrix, a, b, N);
                    a++;
                    b--;
                }
            }
            // Вывести полученный массив
            cout << "Полученный массив:" << endl;
            for (int i = 0; i < N; ++i) {
                for (int j = 0; j < N; ++j) {
                    cout << matrix[i][j] << '\t';
                }
                cout << endl;
            }
            cout << "Массив успешно сохранен в файл output.txt." << endl;
            break;
        case 3:
            for (int diag = 0; diag < N * 2; ++diag) {
                for (int i = max(0, diag - N + 1); i <= min(diag, N - 1); ++i)
                {
                    int j = diag - i;
                    if (diag % 2 == 0)
                    {
                        matrix[i][j] = num;
                    }
                    else {
                        matrix[j][i] = num;
                    }
                    ++num;
                }
            }
            if (N % 2 == 0)
            {
                for (int i = 0; i < (N / 2); i++) {
                    swapC(matrix, a, b, N);
                    a++;
                    b--;
                }
            }
            else
            {
                for (int i = 0; i < (N - 1) / 2; i++) {
                    swapC(matrix, a, b, N);
                    a++;
                    b--;
                }
            }
            // Вывести полученный массив
            cout << "Полученный массив:" << endl;
            for (int i = 0; i < N; ++i) {
                for (int j = 0; j < N; ++j) {
                    cout << matrix[i][j] << '\t';
                }
                cout << endl;
            }
            cout << "Массив успешно сохранен в файл output.txt." << endl;
            break;
        case 4:
            // Заполнить массив числами от 1 до N^2 по возрастанию "змейкой"
            for (int diag = 0; diag < N * 2; ++diag) {
                for (int i = max(0, diag - N + 1); i <= min(diag, N - 1); ++i) {
                    int j = diag - i;
                    if (diag % 2 == 0) {
                        matrix[i][j] = num4;
                    }
                    else {
                        matrix[j][i] = num4;
                    }
                    --num4;
                }
            }
            // Вывести полученный массив
            cout << "Полученный массив:" << endl;
            for (int i = 0; i < N; ++i) {
                for (int j = 0; j < N; ++j) {
                    cout << matrix[i][j] << '\t';
                }
                cout << endl;
            }
            cout << "Массив успешно сохранен в файл output.txt." << endl;
            break;
        default:
            cout << "Введите число от 1 до 4!";
            break;
        }


        // Открыть файл
        ofstream outputFile("output.txt");
        if (!outputFile.is_open()) {
            cout << "Не удалось открыть файл для записи." << endl;
            return 1;
        }

        // Записать массив в файл
        for (int i = 0; i < N; ++i) {
            for (int j = 0; j < N; ++j) {
                outputFile << matrix[i][j] << '\t';
            }
            outputFile << '\n';
        }
        outputFile.close();
        // Освободить выделенную память для массива
        for (int i = 0; i < N; ++i) {
            delete[] matrix[i];
        }
        delete[] matrix;
        cout << "для повторения нажми 5: ";
        cin >> povtor;
    }
        return 0;
}
