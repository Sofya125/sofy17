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
