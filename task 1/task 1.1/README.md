# main.java 

public class Main {
    public static void main(String[] args) {
        Calculator calc = Calculator.instance.get();

        int a = calc.plus.apply(1, 2);
        int b = calc.minus.apply(1, 1);
        int c = calc.devide.apply(a, b);

        calc.println.accept(c); // Вывод: 0 (вместо ошибки деления на ноль)
    }
}

# Calculator.java

import java.util.function.BinaryOperator;
import java.util.function.Consumer;
import java.util.function.Supplier;
import java.util.function.UnaryOperator;

public class Calculator {
    static Supplier<Calculator> instance = Calculator::new;

    BinaryOperator<Integer> plus = (x, y) -> x + y;
    BinaryOperator<Integer> minus = (x, y) -> x - y;
    // BinaryOperator<Integer> devide = (x, y) -> x / y; Если так оставить то будет ошибка деления на 0

    BinaryOperator<Integer> devide = (x, y) -> y != 0 ? x / y : 0; // Обработка деления на ноль
    UnaryOperator<Integer> pow = x -> x * x;
    UnaryOperator<Integer> abs = x -> x > 0 ? x : x * -1;
    Consumer<Integer> println = x -> System.out.println(x);
}

Код выдавал ошибку из-за деления на 0, можно было обернуть try-catch для ловли исключения либо сделать обработку в лямбда-выражение: 
BinaryOperator<Integer> devide = (x, y) -> y != 0 ? x / y : 0;