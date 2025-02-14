//Задание 7
#include <iostream>
#include <fstream>
#include <sstream>
#include <vector>
#include <string>
#include <numeric>

struct Student {
    std::string name;
    std::vector<int> grades;
};

void readDataFromFile(const std::string& filename, std::vector<Student>& students) {
    std::ifstream file(filename);
    std::string line;

    while (std::getline(file, line)) {
        std::istringstream ss(line);
        Student student;
        std::getline(ss, student.name, ',');

        for (std::string grade; std::getline(ss, grade, ',');) {
            student.grades.push_back(std::stoi(grade));
        }
        
        students.push_back(student);
    }
}

void printStudents(const std::vector<Student>& students) {
    for (const auto& student : students) {
        std::cout << "Имя: " << student.name << " Оценки: ";
        for (int grade : student.grades) {
            std::cout << grade << " ";
        }
        double average = std::accumulate(student.grades.begin(), student.grades.end(), 0.0) / student.grades.size();
        std::cout << "Средний балл: " << average << std::endl;
    }
}

int main() {
    std::vector<Student> students;
    std::cout << "Введите имя файла с данными (например, data.csv): ";
    std::string filename;
    std::cin >> filename;

    readDataFromFile(filename, students);
    printStudents(students);

    return 0;
}

Задание по варианту:
#include <iostream>
#include <string>
#include <vector>

std::string convertToBase(int number, int base) {
    if (base < 2 || base > 16) {
        return "Ошибка: Основание должно быть от 2 до 16.";
    }
    
    std::string result;
    const char* digits = "0123456789ABCDEF";

    do {
        result = digits[number % base] + result;
        number /= base; 
    } while (number > 0);

    return result.empty() ? "0" : result;
}

int main() 
{
    int number, base;

    std::cout << "Введите десятичное число: ";
    std::cin >> number;
    std::cout << "Введите основание (от 2 до 16): ";
    std::cin >> base;

    std::string convertedNumber = convertToBase(number, base);
    std::cout << "Число " << number << " в системе счисления с основанием " << base << " равно: " << convertedNumber << std::endl;

    return 0;
}
