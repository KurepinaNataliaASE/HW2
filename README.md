import java.util.Scanner;

public class Calculator {
    private Scanner scanner;

    public Calculator() {
        this.scanner = new Scanner(System.in);
    }

    public void start() {
        System.out.println("Добро пожаловать в консольный калькулятор!");
        System.out.println("Поддерживаемые операции: +, -, *, /");

        while (true) {
            System.out.println("Введите выражение (например, '5 + 3') или 'exit' для выхода:");
            String input = scanner.nextLine();

            if ("exit".equalsIgnoreCase(input)) {
                break;
            }

            Operation operation = parseOperation(input);

            if (operation != null) {
                double result = operation.calculate();
                System.out.println("Результат: " + result);
            }
        }

        System.out.println("Выход из программы...");
    }

    private Operation parseOperation(String input) {
        String[] parts = input.split(" ");
        if (parts.length != 3) {
            System.out.println("Ошибка: неверный формат ввода.");
            return null;
        }

        try {
            double operand1 = Double.parseDouble(parts[0]);
            double operand2 = Double.parseDouble(parts[2]);
            char operator = parts[1].charAt(0);

            switch (operator) {
                case '+':
                    return new Addition(operand1, operand2);
                case '-':
                    return new Subtraction(operand1, operand2);
                case '*':
                    return new Multiplication(operand1, operand2);
                case '/':
                    return new Division(operand1, operand2);
                default:
                    System.out.println("Ошибка: неверная операция.");
                    return null;
            }
        } catch (NumberFormatException e) {
            System.out.println("Ошибка: неверный формат числа.");
            return null;
        }
    }
}


public abstract class Operation {
    protected double operand1;
    protected double operand2;

    public Operation(double operand1, double operand2) {
        this.operand1 = operand1;
        this.operand2 = operand2;
    }

    public abstract double calculate();
}


public class Addition extends Operation {
    public Addition(double operand1, double operand2) {
        super(operand1, operand2);
    }

    @Override
    public double calculate() {
        return operand1 + operand2;
    }
}

public class Subtraction extends Operation {
    public Subtraction(double operand1, double operand2) {
        super(operand1, operand2);
    }

    @Override
    public double calculate() {
        return operand1 - operand2;
    }
}

public class Multiplication extends Operation {
    public Multiplication(double operand1, double operand2) {
        super(operand1, operand2);
    }

    @Override
    public double calculate() {
        return operand1 * operand2;
    }
}

public class Division extends Operation {
    public Division(double operand1, double operand2) {
        super(operand1, operand2);
    }

    @Override
    public double calculate() {
        if (operand2 == 0) {
            throw new ArithmeticException("Ошибка: деление на ноль.");
        }
        return operand1 / operand2;
    }
}


public class ExpressionValidator {
    public boolean isValid(String expression) {
        String[] parts = expression.split(" ");
        return parts.length == 3 && validateOperands(parts[0], parts[2]) && validateOperator(parts[1]);
    }

    private boolean validateOperands(String operand1, String operand2) {
        try {
            Double.parseDouble(operand1);
            Double.parseDouble(operand2);
            return true;
        } catch (NumberFormatException e) {
            return false;
        }
    }

    private boolean validateOperator(String operator) {
        return "+-*/".contains(operator);
    }
}


private Operation parseOperation(String input) {
    ExpressionValidator validator = new ExpressionValidator();
    if (!validator.isValid(input)) {
        System.out.println("Ошибка: неверный формат ввода.");
        return null;
    }

    String[] parts = input.split(" ");
    double operand1 = Double.parseDouble(parts[0]);
    double operand2 = Double.parseDouble(parts[2]);
    char operator = parts[1].charAt(0);

    switch (operator) {
        case '+':
            return new Addition(operand1, operand2);
        case '-':
            return new Subtraction(operand1, operand2);
        case '*':
            return new Multiplication(operand1, operand2);
        case '/':
            return new Division(operand1, operand2);
        default:
            System.out.println("Ошибка: неверная операция.");
            return null;
    }
}
