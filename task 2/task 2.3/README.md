# Без Stream API, используем коллекции
# main.java

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

public class Main {

    public static void main(String[] args) {
        List<Integer> intList = Arrays.asList(1, 2, 5, 16, -1, -2, 0, 32, 3, 5, 8, 23, 4);
        List<Integer> sortedList = new ArrayList<>();

        for (int i = 0; i < intList.size(); i++) {
            if (intList.get(i) > 0 && (intList.get(i) % 2 == 0)) {
                sortedList.add(intList.get(i));
            }
        }
        Collections.sort(sortedList);
        for (int x : sortedList) {
            System.out.println(x);
        }
    }
}

# Используем стримы из библиотеки Stream API.
# StreamMain

import java.util.Arrays;
import java.util.Comparator;
import java.util.List;
import java.util.stream.Stream;

public class StreamMain {

    public static void main(String[] args) {
        List<Integer> intList = Arrays.asList(1, 2, 5, 16, -1, -2, 0, 32, 3, 5, 8, 23, 4);
        Stream<Integer> stream = intList.stream();
        stream
                .filter(x -> x > 0)
                .filter(x -> x % 2 == 0)
                .sorted(Comparator.naturalOrder())
                .forEach(System.out::println);
    }
}