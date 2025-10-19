import java.util.Scanner;

public class Main {
    private static int totalEarnings = 0;
    private static int totalSpending = 0;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while(true) {
            System.out.println("Выберите операцию и введите её номер:");
            System.out.println("1. Добавить новый доход");
            System.out.println("2. Добавить новый расход");
            System.out.println("3. Выбрать систему налогообложения");

            String input = scanner.nextLine();

            if (input.equals("end")) {
                System.out.println("Программа завершена!");
                break;
            }

            try {
                int choice = Integer.parseInt(input);
                switch(choice) {
                    case 1:
                        addEarnings(scanner);
                        break;
                    case 2:
                        addSpending(scanner);
                        break;
                    case 3:
                        calculateTax(scanner);
                        break;
                    default:
                        System.out.println("Неверное число.");
                }
            } catch (NumberFormatException e) {
                System.out.println("Ошибка: введите число от 1 до 3 или 'end'.");
            }
        }
    }

    private static void addEarnings(Scanner scanner) {
        System.out.println("Введите сумму дохода:");
        try {
            int income = Integer.parseInt(scanner.nextLine());
            if (income < 0) {
                System.out.println("Сумма дохода не должна быть отрицательной.");
                return;
            }
            totalEarnings += income;
            System.out.println("Доход добавлен: " + income + " рублей");
            System.out.println("Общий доход: " + totalEarnings + " рублей");
        } catch (NumberFormatException e) {
            System.out.println("Некорректная сумма. Введите целое число.");
        }
    }

    private static void addSpending(Scanner scanner) {
        System.out.println("Введите сумму расхода:");
        try {
            int spend = Integer.parseInt(scanner.nextLine());
            if (spend < 0) {
                System.out.println("Сумма расхода не должна быть отрицательной.");
                return;
            }
            totalSpending += spend;
            System.out.println("Расход добавлен: " + spend + " рублей");
            System.out.println("Общий расход: " + totalSpending + " рублей");
        } catch (NumberFormatException e) {
            System.out.println("Некорректная сумма. Введите целое число.");
        }
    }

    private static void calculateTax(Scanner scanner) {
        System.out.println("Выберите систему налогообложения:");
        System.out.println("1. УСН 6% (доходы)");
        System.out.println("2. УСН 15% (доходы - расходы)");

        try {
            int choice = Integer.parseInt(scanner.nextLine());
            int tax = 0;

            switch(choice) {
                case 1:
                    tax = totalEarnings * 6 / 100;
                    System.out.println("Налог по УСН 6%: " + tax + " рублей");
                    break;
                case 2:
                    int profit = totalEarnings - totalSpending;
                    tax = ( profit  / 100 ) * 15 ;
                    System.out.println("Налог по УСН 15%: " + tax + " рублей");
                    break;
                default:
                    System.out.println("Неверный выбор. Введите 1 или 2.");
            }
        } catch (NumberFormatException e) {
            System.out.println("Ошибка: введите число 1 или 2.");
        }
    }

}
