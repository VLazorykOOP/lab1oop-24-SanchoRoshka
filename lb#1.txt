#include <iostream>
#include <time.h>
#include <fstream>
#include <ios>

using namespace std;

const int sizeMax = 200;

void MainMenu()
{
    cout << "Main Menu\n";
    cout << "1. Task 1\n";
    cout << "2. Task 2\n";
}

void MenuInput()
{
    cout << "Menu Input\n";
    cout << "1. Console all\n";
    cout << "2. Console - size, array - random\n";
}

int GetSizeArray(const int max_size)
{
    int size = 0;
    cout << "Input size of the array (0 < size < " << max_size << "): ";
    cin >> size;
    return size;
}

int GetInputArray(int size, int array[])
{
    for (int i = 0; i < size; i++)
    {
        cout << "Array[" << i << "]: ";
        cin >> array[i];
    }
    return size;
}

int GenerateRandom(int size, int array[])
{
    srand(time(NULL));
    cout << "\nArray:\n";
    for (int i = 0; i < size; i++)
    {
        array[i] = rand() % 100 - 50;
        cout << array[i] << "   ";
    }
    return size;
}

void WriteTextFile(int size, int* array, const char* fileName)
{
    ofstream fout(fileName);
    if (fout.fail()) return;
    fout << size << endl;
    for (int i = 0; i < size; i++)
        fout << array[i] << "   ";
    fout.close(); //
}

void WriteBinaryFile(int size, int* array, const char* fileName)
{
    ofstream bfout(fileName, ios_base::binary);
    if (bfout.fail()) return;
    bfout.write((const char*)&size, sizeof(int));
    std::streamsize  count = static_cast<std::streamsize>(size) * sizeof(double);
    bfout.write((const char*)array, count);
    bfout.close();
}

void Multiply(int size, int array[]) {
    int middle_index = size / 2;
    cout << middle_index << endl;
    for (int i = 0; i < size; i++)
    {
        if (i < middle_index) {
            array[i] = array[i] * 2;
        }
        else
        {
            array[i] = array[i] * 3;
        }
    }
    for (int i = 0; i < size; i++)
    {
        cout << "Arr[" << i << "]\t" << array[i] << endl;
    }
}

void FindMinPositive(int size, int array[]) {
    int min = INT_MAX;
    int index = -1;
    for (int i = 0; i < size; i++) {
        if (array[i] < 0) {
            for (int j = i; j < size; j++)
            {
                if (array[j] > 0 && array[j] % 2 == 0) {
                    if (array[j] < min) {
                        min = array[j];
                        index = j;
                    }
                }
            }
        }

    }
    if (index != -1) {
        cout << "Min " << min << " index " << index << endl;
    }
    else {
        cout << "No such value found." << endl;
    }
}

int main()
{
    int array[sizeMax];
    int* dynamic_array = nullptr;
    int choice, size;
    MainMenu();
    cin >> choice;
    switch (choice)
    {
    case 1://task 1
        MenuInput();
        cin >> choice;
        switch (choice)
        {
        case 1:// console
            cout << "1. Local\n2. Dynamic\n";
            cin >> choice;
            switch (choice)
            {
            case 1:
                size = GetSizeArray(sizeMax);
                GetInputArray(size, array);
                Multiply(size, array);
                WriteTextFile(size, array, "file.txt");
                WriteBinaryFile(size, array, "bin.txt");
                break;
            case 2:
                size = GetSizeArray(sizeMax);
                dynamic_array = new int[size];
                GetInputArray(size, dynamic_array);
                Multiply(size, dynamic_array);
                WriteTextFile(size, dynamic_array, "file.txt");
                WriteBinaryFile(size, dynamic_array, "bin.txt");
                delete[] dynamic_array;
                break;
            }
            break;
        case 2://random
            cout << "1. Local\n2. Dynamic\n";
            cin >> choice;
            switch (choice)
            {
            case 1:
                size = GetSizeArray(sizeMax);
                GenerateRandom(size, array);
                Multiply(size, array);
                WriteTextFile(size, array, "file.txt");
                WriteBinaryFile(size, array, "bin.txt");
                break;
            case 2:
                size = GetSizeArray(sizeMax);
                dynamic_array = new int[size];
                GenerateRandom(size, dynamic_array);
                Multiply(size, dynamic_array);
                WriteTextFile(size, dynamic_array, "file.txt");
                WriteBinaryFile(size, dynamic_array, "bin.txt");
                delete[] dynamic_array;
                break;
            }
            break;
        }
        break;

    case 2:// Task 2
        MenuInput();
        cin >> choice;
        switch (choice)
        {
        case 1:// console
            cout << "1. Local\n2. Dynamic\n";
            cin >> choice;
            switch (choice)
            {
            case 1:
                size = GetSizeArray(sizeMax);
                GetInputArray(size, array);
                FindMinPositive(size, array);
                WriteTextFile(size, array, "file.txt");
                WriteBinaryFile(size, array, "bin.txt");
                break;
            case 2:
                size = GetSizeArray(sizeMax);
                dynamic_array = new int[size];
                GetInputArray(size, dynamic_array);
                FindMinPositive(size, dynamic_array);
                WriteTextFile(size, dynamic_array, "file.txt");
                WriteBinaryFile(size, dynamic_array, "bin.txt");
                delete[] dynamic_array;
                break;
            }
            break;
        case 2://random
            cout << "1. Local\n2. Dynamic\n";
            cin >> choice;
            switch (choice)
            {
            case 1:
                size = GetSizeArray(sizeMax);
                GenerateRandom(size, array);
                FindMinPositive(size, array);
                WriteTextFile(size, array, "file.txt");
                WriteBinaryFile(size, array, "bin.txt");
                break;
            case 2:
                size = GetSizeArray(sizeMax);
                dynamic_array = new int[size];
                GenerateRandom(size, dynamic_array);
                FindMinPositive(size, dynamic_array);
                WriteTextFile(size, dynamic_array, "file.txt");
                WriteBinaryFile(size, dynamic_array, "bin.txt");
                delete[] dynamic_array;
                break;
            }
            break;
        }
        break;
    }

    return 0;
}
