# QUICKDZ
Structure sorting by Hoare method С++
#include <iostream>
using namespace std;


struct School // объявление структуры
{
    int number;
    int receipt;
    int expense;
    int remains;
};


void quickSort(struct School* data, int low, int high) // создание функции сортировки
{
    int i = low; // первый элемент
    int j = high; // последний элемент
    int pivot = data[(i + j) / 2].remains; // центральный элемент
    School temp;
    while (i <= j)
    {
        while (data[i].remains < pivot)
            i++;
        while (data[j].remains > pivot)
            j--;
        if (i <= j)
        {
            temp = data[i];
            data[i] = data[j];
            data[j] = temp;
            i++;
            j--;
        }
    }
    if (j > low)
        quickSort(data, low, j);
    if (i < high)
        quickSort(data, i, high);
}


int main()
{
    int n;
    cout << "Введите кол-во школ: ";
    cin >> n;
    School *a = new School[n]; // объявление динамического типа памяти для массива структур
    for (int i = 0; i < n; i++) // ввод
    {
        cout << "Введите номер школы: ";
        cin >> a[i].number;
        cout << "Введите выделенную сумму: ";
        cin >> a[i].receipt;
        cout << "Введите потраченную сумму: ";
        cin >> a[i].expense;
        a[i].remains = a[i].receipt - a[i].expense;
    }
    quickSort(a, 0, n - 1); // вызов функции сортировки
    for (int i = n - 1; i >= 0; i--) // вывод в обратном порядке
    {
            cout << "Номер школы: " << a[i].number;
            cout << "\n";
            cout << "Остаток денежных средств: " << a[i].remains;
            cout << "\n";
    }
    delete []a; // удаление структур
    return 0;
}
