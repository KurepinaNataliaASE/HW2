import java.util.Scanner;

public class ConsoleCalculator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
  
        System.out.println("Добро пожаловать в консольный калькулятор!");
        System.out.println("Поддерживаемые операции: +, -, *, /, //, ^, %");
  
        while (true) {
            System.out.println("Введите выражение (например, '5 + 3') или 'exit' для выхода:");
            String input = scanner.nextLine();
  
            if ("exit".equalsIgnoreCase(input)) {
                break;
            }
  
            String[] parts = input.split(" ");
            if (parts.length != 3) {
                System.out.println("Ошибка: неверный формат ввода.");
                continue;
            }
  
            try {
                double operand1 = Double.parseDouble(parts[0]);
                double operand2 = Double.parseDouble(parts[2]);
                char operation = parts[1].charAt(0);
  
                double result = performOperation(operation, operand1, operand2);
                System.out.println("Результат: " + result);
            } catch (NumberFormatException e) {
                System.out.println("Ошибка: неверный формат числа.");
            } catch (IllegalArgumentException e) {
                System.out.println(e.getMessage());
            }
        }
  
        System.out.println("Выход из программы...");
    }

    private static double performOperation(char operation, double operand1, double operand2) throws IllegalArgumentException {
        switch (operation) {
            case '+':
                return sum(operand1, operand2);
            case '-':
                return subtract(operand1, operand2);
            case '*':
                return multiply(operand1, operand2);
            case '/':
                return divide(operand1, operand2);
            case '^':
                return power(operand1, operand2);
            case '%':
                return modulo(operand1, operand2);
            default:
                throw new IllegalArgumentException("Неподдерживаемая операция.");
        }
    }

    private static double sum(double a, double b) {
        return a + b;
    }

    private static double subtract(double a, double b) {
        return a - b;
    }

    private static double multiply(double a, double b) {
        return a * b;
    }

    private static double divide(double a, double b) throws IllegalArgumentException {
        if (b == 0) {
            throw new IllegalArgumentException("Ошибка: деление на ноль.");
        }
        return a / b;
    }

    private static double power(double a, double b) {
        return Math.pow(a, b);
    }

    private static double modulo(double a, double b) throws IllegalArgumentException {
        if (b == 0) {
            throw new IllegalArgumentException("Ошибка: деление на ноль.");
        }
        return a % b;
    }
}
