import java.util.Scanner;

public class Main {
public static void main(String[] args) {
// Создание базы данных сущностей в виде Map
Map<Long, Book> booksMap = new HashMap<>();

scss
Copy code
    // Добавление минимум 10 сущностей
    for (int i = 0; i < 10; i++) {
        Book book = new Book.Builder()
                .setId((long) i)
                .setName("Book " + i)
                .setDescription("Description of Book " + i)
                .setIsdn("ISBN " + i)
                .setPrice(10.0 + i)
                .setDiscount(0.2)
                .setNumber(10 + i)
                .build();

        booksMap.put(book.id, book);
    }

    // Вывод информации о всех книгах
    for (Book book : booksMap.values()) {
        System.out.println(book);
    }

    Scanner scanner = new Scanner(System.in);
    int choice = 0;

    do {
        System.out.println("Выберите действие:");
        System.out.println("1. Посчитать все книги");
        System.out.println("2. Добавить книгу");
        System.out.println("3. Удалить книгу");
        System.out.println("4. Выйти");

        choice = scanner.nextInt();

        switch (choice) {
            case 1:
                System.out.println("Всего книг: " + booksMap.size());
                break;

            case 2:
                // Добавляем новую книгу
                Book newBook = new Book.Builder()
                        .setId((long) booksMap.size())
                        .setName("New Book")
                        .setDescription("Description of New Book")
                        .setIsdn("New ISBN")
                        .setPrice(15.0)
                        .setDiscount(0.1)
                        .setNumber(5)
                        .build();

                booksMap.put(newBook.id, newBook);
                System.out.println("Новая книга добавлена: " + newBook);
                break;

            case 3:
                // Удаляем книгу
                System.out.println("Введите ID книги для удаления:");
                Long idToRemove = scanner.nextLong();
                if (booksMap.containsKey(idToRemove)) {
                    booksMap.remove(idToRemove);
                    System.out.println("Книга успешно удалена");
                } else {
                    System.out.println("Книга с таким ID не найдена");
                }
                break;

            case 4:
                System.out.println("Выход из программы");
                break;

            default:
                System.out.println("Некорректный выбор, повторите попытку");
        }
    } while (choice != 4);
}







import java.util.HashMap;
import java.util.Map;

// Сущность книги
class Book {
    private Long id;
    private String name;
    private String description;
    private String isdn;
    private double price;
    private double discount;
    private int number;

    // Приватный конструктор для использования Builder
    private Book() {}

    // Builder для создания экземпляра книги
    static class Builder {
        private final Book book = new Book();

        public Builder setId(Long id) {
            book.id = id;
            return this;
        }

        public Builder setName(String name) {
            book.name = name;
            return this;
        }

        public Builder setDescription(String description) {
            book.description = description;
            return this;
        }

        public Builder setIsdn(String isdn) {
            book.isdn = isdn;
            return this;
        }

        public Builder setPrice(double price) {
            book.price = price;
            return this;
        }

        public Builder setDiscount(double discount) {
            book.discount = discount;
            return this;
        }

        public Builder setNumber(int number) {
            book.number = number;
            return this;
        }

        public Book build() {
            return book;
        }
    }

    @Override
    public String toString() {
        return "Book{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", description='" + description + '\'' +
                ", isdn='" + isdn + '\'' +
                ", price=" + price +
                ", discount=" + discount +
                ", number=" + number +
                '}';
    }
}

public class Main {
    public static void main(String[] args) {
        // Создание базы данных сущностей в виде Map
        Map<Long, Book> booksMap = new HashMap<>();

        // Добавление минимум 10 сущностей
        for (int i = 0; i < 10; i++) {
            Book book = new Book.Builder()
                    .setId((long) i)
                    .setName("Book " + i)
                    .setDescription("Description of Book " + i)
                    .setIsdn("ISBN " + i)
                    .setPrice(10.0 + i)
                    .setDiscount(0.2)
                    .setNumber(10 + i)
                    .build();

            booksMap.put(book.id, book);
        }

        // Вывод информации о всех книгах
        for (Book book : booksMap.values()) {
            System.out.println(book);
        }
    }
}






```java
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

// Сущность Книга
class Book {
    private Long id;
    private String name;
    private String description;
    private String isdn;
    private double price;
    private double discount;
    private int number;

    public static class Builder {
        private Long id;
        private String name;
        private String description;
        private String isdn;
        private double price;
        private double discount;
        private int number;

        public Builder setId(Long id) {
            this.id = id;
            return this;
        }

        public Builder setName(String name) {
            this.name = name;
            return this;
        }

        public Builder setDescription(String description) {
            this.description = description;
            return this;
        }

        public Builder setIsdn(String isdn) {
            this.isdn = isdn;
            return this;
        }

        public Builder setPrice(double price) {
            this.price = price;
            return this;
        }

        public Builder setDiscount(double discount) {
            this.discount = discount;
            return this;
        }

        public Builder setNumber(int number) {
            this.number = number;
            return this;
        }

        public Book build() {
            Book book = new Book();
            book.id = this.id;
            book.name = this.name;
            book.description = this.description;
            book.isdn = this.isdn;
            book.price = this.price;
            book.discount = this.discount;
            book.number = this.number;
            return book;
        }
    }

    @Override
    public String toString() {
        return "Book{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", description='" + description + '\'' +
                ", isdn='" + isdn + '\'' +
                ", price=" + price +
                ", discount=" + discount +
                ", number=" + number +
                '}';
    }
}

public class Main {
    public static void main(String[] args) {
        Map<Long, Book> bookMap = new HashMap<>();
        Scanner scanner = new Scanner(System.in);

        for (int i = 0; i < 10; i++) {
            System.out.println("Enter book details for book " + i);

            System.out.print("ID: ");
            Long id = scanner.nextLong();
            scanner.nextLine();

            System.out.print("Name: ");
            String name = scanner.nextLine();

            System.out.print("Description: ");
            String description = scanner.nextLine();

            System.out.print("ISBN: ");
            String isdn = scanner.next();
            scanner.nextLine();

            System.out.print("Price: ");
            double price = scanner.nextDouble();

            System.out.print("Discount: ");
            double discount = scanner.nextDouble();

            System.out.print("Number: ");
            int number = scanner.nextInt();

            Book book = new Book.Builder()
                    .setId(id)
                    .setName(name)
                    .setDescription(description)
                    .setIsdn(isdn)
                    .setPrice(price)
                    .setDiscount(discount)
                    .setNumber(number)
                    .build();

            bookMap.put(book.getId(), book);
        }

        System.out.println("Book details entered:");
        for (Map.Entry<Long, Book> entry : bookMap.entrySet()) {
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
        }
    }
}
```






import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;

import java.util.Scanner;

class StoreMaterial {
    private int ID;
    private String name;
    private String description;
    private double price;
    private int number;
    private int numberCard;
    private int idCard;

    public StoreMaterial(int ID, String name, String description, double price, int number, int numberCard, int idCard) {
        this.ID = ID;
        this.name = name;
        this.description = description;
        this.price = price;
        this.number = number;
        this.numberCard = numberCard;
        this.idCard = idCard;
    }

    public String toString() {
        try {
            return new ObjectMapper().writeValueAsString(this);
        } catch (JsonProcessingException e) {
            e.printStackTrace();
            return "";
        }
    }
}

public class Main {
    public static void main(String[] args) {
        StoreMaterial material1 = new StoreMaterial(1, "Bricks", "Red bricks for construction", 10.0, 100, 12345, 54321);
        StoreMaterial material2 = new StoreMaterial(2, "Cement", "High quality cement", 15.0, 50, 54321, 12345);

        System.out.println("Available materials:");
        System.out.println("1. " + material1.toString());
        System.out.println("2. " + material2.toString());

        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the ID of the material you want to order: ");
        int chosenMaterialID = scanner.nextInt();

        System.out.print("Enter the quantity of the material you want to order: ");
        int quantity = scanner.nextInt();

        if (chosenMaterialID == 1) {
            material1.number -= quantity;
        } else if (chosenMaterialID == 2) {
            material2.number -= quantity;
        }

        System.out.println("Order details:");
        if (chosenMaterialID == 1) {
            System.out.println("Ordered material: " + material1.name);
            System.out.println("Quantity: " + quantity);
            System.out.println("Total Price: " + (material1.price * quantity));
        } else if (chosenMaterialID == 2) {
            System.out.println("Ordered material: " + material2.name);
            System.out.println("Quantity: " + quantity);
            System.out.println("Total Price: " + (material2.price * quantity));
        }
    }
}






```java
import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;

public class BuildingMaterialStore {
    private int ID;
    private String name;
    private String description;
    private double price;
    private int number;
    private int numberCard;
    private int idCard;

    public BuildingMaterialStore(int ID, String name, String description, double price, int number, int numberCard, int idCard) {
        this.ID = ID;
        this.name = name;
        this.description = description;
        this.price = price;
        this.number = number;
        this.numberCard = numberCard;
        this.idCard = idCard;
    }

    @Override
    public String toString() {
        ObjectMapper objectMapper = new ObjectMapper();
        try {
            return objectMapper.writeValueAsString(this);
        } catch (JsonProcessingException e) {
            e.printStackTrace();
        }
        return null;
    }

    public static void main(String[] args) {
        BuildingMaterialStore store = new BuildingMaterialStore(1, "Building Supplies", "Various materials for construction", 100.0, 50, 1234, 5678);
        System.out.println(store.toString());
    }
}
```






import java.util.Scanner;

public class MatrixDeterminant {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Введите количество строк матрицы: ");
        int x = scanner.nextInt();
        System.out.print("Введите количество столбцов матрицы: ");
        int y = scanner.nextInt();

        int[][] matrix = new int[x][y];
        System.out.println("Введите элементы матрицы:");

        for (int i = 0; i < x; i++) {
            for (int j = 0; j < y; j++) {
                while (!scanner.hasNextInt()) {
                    System.out.println("Ошибка: введите число");
                    scanner.next();
                }
                matrix[i][j] = scanner.nextInt();
            }
        }

        System.out.println("Определитель матрицы: " + determinant(matrix));
    }

    public static int determinant(int[][] matrix) {
        int n = matrix.length;

        if (n == 1) {
            return matrix[0][0];
        }

        int det = 0;
        int sign = 1;

        for (int i = 0; i < n; i++) {
            int[][] subMatrix = new int[n - 1][n - 1];

            for (int j = 1; j < n; j++) {
                for (int k = 0; k < n; k++) {
                    if (k < i) {
                        subMatrix[j - 1][k] = matrix[j][k];
                    } else if (k > i) {
                        subMatrix[j - 1][k - 1] = matrix[j][k];
                    }
                }
            }

            det += sign * matrix[0][i] * determinant(subMatrix);
            sign = -sign;
        }

        return det;
    }
}



import java.util.Scanner;

public class MatrixDeterminant {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Введите размерность матрицы: ");
        int n = scanner.nextInt();

        int[][] matrix = new int[n][n];
        System.out.println("Введите элементы матрицы:");

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = scanner.nextInt();
            }
        }

        System.out.println("Определитель матрицы: " + determinant(matrix));
    }

    public static int determinant(int[][] matrix) {
        int n = matrix.length;

        if (n == 1) {
            return matrix[0][0];
        }

        int det = 0;
        int sign = 1;

        for (int i = 0; i < n; i++) {
            int[][] subMatrix = new int[n - 1][n - 1];

            for (int j = 1; j < n; j++) {
                for (int k = 0; k < n; k++) {
                    if (k < i) {
                        subMatrix[j - 1][k] = matrix[j][k];
                    } else if (k > i) {
                        subMatrix[j - 1][k - 1] = matrix[j][k];
                    }
                }
            }

            det += sign * matrix[0][i] * determinant(subMatrix);
            sign = -sign;
        }

        return det;
    }
}



```java
public class MatrixDeterminant {
    
    public static void main(String[] args) {
        int[][] matrix = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
        
        int determinant = calculateDeterminant(matrix);
        
        System.out.println("Determinant of the matrix is: " + determinant);
    }
    
    public static int calculateDeterminant(int[][] matrix) {
        int determinant = 0;
        
        if(matrix.length == 2) {
            determinant = matrix[0][0]*matrix[1][1] - matrix[0][1]*matrix[1][0];
        } else {
            for(int i = 0; i < matrix.length; i++) {
                determinant += Math.pow(-1, i) * matrix[0][i] * calculateDeterminant(getSubMatrix(matrix, 0, i));
            }
        }
        
        return determinant;
    }
    
    public static int[][] getSubMatrix(int[][] matrix, int row, int col) {
        int size = matrix.length - 1;
        int[][] subMatrix = new int[size][size];
        
        int r = 0, c = 0;
        for(int i = 0; i < matrix.length; i++) {
            if(i == row) continue;
            for(int j = 0; j < matrix.length; j++) {
                if(j == col) continue;
                subMatrix[r][c] = matrix[i][j];
                c++;
            }
            r++;
            c = 0;
        }
        
        return subMatrix;
    }
}
```




public class TwoDimensionalArray {
  
    public static int determinant(int[][] matrix) {
        int rows = matrix.length;
        int columns = matrix[0].length;
        if (rows != columns) {
            System.out.println("Error: Matrix is not square.");
            return 0;
        }

        if (rows == 1) {
            return matrix[0][0];
        }

        if (rows == 2) {
            return matrix[0][0] * matrix[1][1] - matrix[0][1] * matrix[1][0];
        }

        int det = 0;
        for (int i = 0; i < rows; i++) {
            int[][] subMatrix = new int[rows - 1][columns - 1];
            for (int j = 1; j < rows; j++) {
                for (int k = 0; k < columns; k++) {
                    if (k < i) {
                        subMatrix[j - 1][k] = matrix[j][k];
                    } else if (k > i) {
                        subMatrix[j - 1][k - 1] = matrix[j][k];
                    }
                }
            }
            det += Math.pow(-1, i) * matrix[0][i] * determinant(subMatrix);
        }
        return det;
    }

    public static void main(String[] args) {
        // Your existing code for inputting matrix elements and printing the matrix

        // Calculate and print the determinant of the matrix
        System.out.println("The determinant of the matrix is: " + determinant(matrix));
    }
}



import java.util.InputMismatchException;
import java.util.Scanner;

public class TwoDimensionalArray {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        while (true) {
            System.out.print("Enter number of rows: ");
            int rows = 0;
            try {
                rows = scanner.nextInt();
            } catch (InputMismatchException e) {
                System.out.println("Error: Please enter a valid number.");
                scanner.next(); // Clear the invalid input
                continue;
            }
            
            System.out.print("Enter number of columns: ");
            int columns = 0;
            try {
                columns = scanner.nextInt();
            } catch (InputMismatchException e) {
                System.out.println("Error: Please enter a valid number.");
                scanner.next(); // Clear the invalid input
                continue;
            }
            
            int[][] matrix = new int[rows][columns];
            
            System.out.println("Enter elements of the matrix: ");
            for (int i = 0; i < rows; i++) {
                for (int j = 0; j < columns; j++) {
                    try {
                        matrix[i][j] = scanner.nextInt();
                    } catch (InputMismatchException e) {
                        System.out.println("Error: Please enter a valid number.");
                        scanner.next(); // Clear the invalid input
                        continue;
                    }
                }
            }
            
            System.out.println("The matrix is: ");
            for (int i = 0; i < rows; i++) {
                for (int j = 0; j < columns; j++) {
                    System.out.print(matrix[i][j] + " ");
                }
                System.out.println();
            }
        }
    }
}






import java.util.InputMismatchException;

public class TwoDimensionalArray {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter number of rows: ");
        int rows = 0;
        try {
            rows = scanner.nextInt();
        } catch (InputMismatchException e) {
            System.out.println("Error: Please enter a valid number.");
            return;
        }
        
        System.out.print("Enter number of columns: ");
        int columns = 0;
        try {
            columns = scanner.nextInt();
        } catch (InputMismatchException e) {
            System.out.println("Error: Please enter a valid number.");
            return;
        }
        
        int[][] matrix = new int[rows][columns];
        
        System.out.println("Enter elements of the matrix: ");
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                try {
                    matrix[i][j] = scanner.nextInt();
                } catch (InputMismatchException e) {
                    System.out.println("Error: Please enter a valid number.");
                    return;
                }
            }
        }
        
        System.out.println("The matrix is: ");
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                System.out.print(matrix[i][j] + " ");
            }
            System.out.println();
        }
    }
}



// Нормализация матрицы от меньшего
int min = matrix[0][0];
for (int i = 0; i < rows; i++) {
    for (int j = 0; j < columns; j++) {
        if (matrix[i][j] < min) {
            min = matrix[i][j];
        }
    }
}

System.out.println("Normalized matrix from smallest element: ");
for (int i = 0; i < rows; i++) {
    for (int j = 0; j < columns; j++) {
        System.out.print((matrix[i][j] - min) + " ");
    }
    System.out.println();
}


import java.util.Scanner;

public class TwoDimensionalArray {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter number of rows: ");
        int rows = scanner.nextInt();
        
        System.out.print("Enter number of columns: ");
        int columns = scanner.nextInt();
        
        int[][] matrix = new int[rows][columns];
        
        System.out.println("Enter elements of the matrix: ");
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                matrix[i][j] = scanner.nextInt();
            }
        }
        
        System.out.println("The matrix is: ");
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                System.out.print(matrix[i][j] + " ");
            }
            System.out.println();
        }
    }
}



import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Получение размеров матрицы от пользователя
        System.out.print("Введите количество строк матрицы: ");
        int rows = scanner.nextInt();
        System.out.print("Введите количество столбцов матрицы: ");
        int cols = scanner.nextInt();

        int[][] matrix = new int[rows][cols];

        // Заполнение матрицы с помощью ввода с консоли
        System.out.println("Введите элементы матрицы:");
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                matrix[i][j] = scanner.nextInt();
            }
        }

        // Вывод матрицы
        System.out.println("Матрица:");
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                System.out.print(matrix[i][j] + " ");
            }
            System.out.println();
        }
    }
}



String numberedInput = "Задание " + taskCount + ": " + input;
                writeToTextFile(numberedInput);
                taskCount++;
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void writeToTextFile(String text) throws IOException {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt", true))) {
            writer.write(text);
            writer.newLine();
        }
    }
}


import java.util.Scanner;
import java.io.FileWriter;
import java.io.IOException;
import java.io.File;

public class BubbleSort {
    public static void main(String[] args) {
        // Создаем объект Scanner для чтения ввода пользователя
        Scanner scanner = new Scanner(System.in);

        // Запрашиваем у пользователя количество чисел в массиве
        System.out.print("Введите количество чисел в массиве: ");
        int length;
        if (scanner.hasNextInt()) {
            length = scanner.nextInt();
        } else {
            System.out.println("Ошибка! Введите число.");
            return;
        }

        // Проверяем, что введенное значение длины массива положительное
        if (length <= 0) {
            System.out.println("Ошибка! Введите положительное число.");
            return;
        }

        // Создаем массив для хранения чисел
        int[] array = new int[length];

        // Запрашиваем у пользователя числа для заполнения массива
        System.out.println("Введите числа для заполнения массива:");
        for (int i = 0; i < length; i++) {
            if (scanner.hasNextInt()) {
                array[i] = scanner.nextInt();
            } else {
                System.out.println("Ошибка! Введите число.");
                return;
            }
        }

        // Проверяем, что не осталось лишних чисел после заполнения массива
        if (scanner.hasNext()) {
            System.out.println("Ошибка! Лишние числа во вводе.");
            return;
        }

        // Сортировка пузырьком
        bubbleSort(array);

        // Запись отсортированного массива в текстовый файл
        writeArrayToFile(array);

        System.out.println("Массив успешно отсортирован и сохранен в файл.");
    }

    public static void bubbleSort(int[] array) {
        int n = array.length;
        for (int i = 0; i < n-1; i++) {
            for (int j = 0; j < n-i-1; j++) {
                if (array[j] > array[j+1]) {
                    // меняем элементы местами
                    int temp = array[j];
                    array[j] = array[j+1];
                    array[j+1] = temp;
                }
            }
        }
    }

    public static void writeArrayToFile(int[] array) {
        try {
            // Создаем объект FileWriter с указанием имени файла
            FileWriter writer = new FileWriter("sorted_array.txt", true);

            // Записываем каждый элемент массива в файл
            for (int i = 0; i < array.length; i++) {
                writer.write(String.valueOf(array[i]));
                writer.write(" ");
            }
            writer.write("\n");

            // Закрываем объект FileWriter
            writer.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}



try {
            // Создаем объект FileWriter с указанием имени файла
            FileWriter writer = new FileWriter("sorted_array.txt", true);

            // Записываем каждый элемент массива в файл
            for (int i = 0; i < array.length; i++) {
                writer.write(String.valueOf(array[i]));
                writer.write(" ");
            }
            writer.write("\n");

            // Закрываем объект FileWriter
            writer.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}



import java.util.Scanner;
import java.io.FileWriter;
import java.io.IOException;

public class BubbleSort {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Ввод длины массива
        System.out.print("Введите длину массива: ");
        while (!scanner.hasNextInt()) {
            System.out.println("Ошибка! Введите число: ");
            scanner.next();
        }
        int length = scanner.nextInt();
        
        // Ввод элементов массива
        int[] arr = new int[length];
        System.out.println("Введите элементы массива:");
        for (int i = 0; i < length; i++) {
            while (!scanner.hasNextInt()) {
                System.out.println("Ошибка! Введите число: ");
                scanner.next();
            }
            arr[i] = scanner.nextInt();
        }

        scanner.close();

        // Проверка на количество элементов массива
        if (arr.length != length) {
            System.out.println("Ошибка! Количество чисел не совпадает с указанной длиной массива.");
            return;
        }

        // Сортировка пузырьком
        for (int i = 0; i < length - 1; i++) {
            for (int j = 0; j < length - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
        
        // Вывод отсортированного массива в консоль и в файл
        try {
            FileWriter writer = new FileWriter("sorted_array.txt");
            System.out.println("Отсортированный массив:");
            for (int i = 0; i < length; i++) {
                System.out.print(arr[i] + " ");
                writer.write(arr[i] + " ");
            }
            writer.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}




import java.util.Arrays;
import java.util.InputMismatchException;
import java.util.Scanner;

public class BubbleSort {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            try {
                System.out.print("Введите длину массива: ");
                int length = scanner.nextInt();
                scanner.nextLine(); // Чтение символа новой строки после ввода числа

                if (length <= 0) {
                    throw new IllegalArgumentException("Длина массива должна быть больше нуля");
                }

                int[] array = new int[length];

                for (int i = 0; i < length; i++) {
                    System.out.print("Введите число для индекса " + i + ": ");
                    array[i] = scanner.nextInt();
                    scanner.nextLine(); // Чтение символа новой строки после ввода числа
                }

                bubbleSort(array);

                System.out.println("Отсортированный массив: " + Arrays.toString(array));
                break;
            } catch (InputMismatchException e) {
                System.out.println("Ошибка: введено некорректное значение");
                scanner.nextLine(); // Сброс буфера сканера
            } catch (IllegalArgumentException e) {
                System.out.println("Ошибка: " + e.getMessage());
            }
        }
    }

    public static void bubbleSort(int[] array) {
        int n = array.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (array[j] > array[j + 1]) {
                    // Swap array[j] and array[j+1]
                    int temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
                }
            }
        }
    }
}




import java.util.Scanner;

public class BubbleSort {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the length of the array: ");
        if (!scanner.hasNextInt()) {
            System.out.println("Error: Invalid input!");
            return;
        }
        int length = scanner.nextInt();

        int[] arr = new int[length];

        System.out.printf("Enter %d numbers for the array:\n", length);
        for (int i = 0; i < length; i++) {
            if (!scanner.hasNextInt()) {
                System.out.println("Error: Invalid input!");
                return;
            }
            arr[i] = scanner.nextInt();
        }

        if (arr.length != length) {
            System.out.println("Error: Length mismatch!");
            return;
        }

        bubbleSort(arr);

        System.out.println("Sorted array:");
        for (int num : arr) {
            System.out.print(num + " ");
        }
        System.out.println();
    }

    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // swap arr[j] and arr[j+1]
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }
}




import java.util.Scanner;

public class BubbleSort {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Введите длину массива: ");
        if (scanner.hasNextInt()) {
            int length = scanner.nextInt();
            if (length >= 0) {
                int[] array = new int[length];
                
                System.out.println("Введите элементы массива:");
                for (int i = 0; i < length; i++) {
                    if (scanner.hasNextInt()) {
                        array[i] = scanner.nextInt();
                    } else {
                        System.out.println("Ошибка: введено некорректное число");
                        return;
                    }
                }
                
                bubbleSort(array);
                
                System.out.println("Отсортированный массив:");
                for (int num : array) {
                    System.out.print(num + " ");
                }
            } else {
                System.out.println("Ошибка: некорректная длина массива");
            }
        } else {
            System.out.println("Ошибка: введена некорректная длина массива");
        }
    }
    
    public static void bubbleSort(int[] array) {
        int length = array.length;
        
        for (int i = 0; i < length - 1; i++) {
            for (int j = 0; j < length - i - 1; j++) {
                if (array[j] > array[j + 1]) {
                    int temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
                }
            }
        }
    }
}




try {
    int number = Integer.parseInt(yourString);

} catch (NumberFormatException ex) {
    System.out.println("Not a valid number!");
}


package ua.com.prologistic;
 
import java.util.Arrays;
import java.util.Scanner;
 
public class BubbleSort {
 
    public static void main(String[] args) {
        int counter, num, array[];
 
        //Создаем объект Scanner для считывания чисел, введенных пользователем
        Scanner input = new Scanner(System.in);
        System.out.println("Введите количество элементов массива: ");
        num = input.nextInt();
 
        // Создаем массив введенного пользователем размера
        array = new int[num];
 
        System.out.println("Введите " + num + " чисел");
 
        //Заполняем массив, вводя элементы в консоль
        for (counter = 0; counter < num; counter++) {
            array[counter] = input.nextInt();
        }
 
        // печатаем массив перед пузырьковой сортировкой
        System.out.println("массив перед пузырьковой сортировкой : " + Arrays.toString(array));
 
        // сортируем массив
        bubbleSort(array);
 
        // печатаем массив после пузырьковой сортировки
        System.out.println("массив после пузырьковой сортировки : " + Arrays.toString(array));
    }
 
    // метод пузырьковой сортировки
    public static void bubbleSort(int[] num) {
        int j;
        boolean flag = true;   // устанавливаем наш флаг в true для первого прохода по массиву
        int temp;   // вспомогательная переменная
 
        while (flag) {
            flag = false;    // устанавливаем флаг в false в ожидании возможного свопа (замены местами)
            for (j = 0; j < num.length - 1; j++) {
                if (num[j] < num[j + 1]) { // измените на > для сортировки по возрастанию
                    temp = num[j];         // меняем элементы местами
                    num[j] = num[j + 1];
                    num[j + 1] = temp;
                    flag = true;  // true означает, что замена местами была проведена
                }
            }
        }
    }
}


public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Введите длину массива: ");
        int length = scanner.nextInt();
        int[] array = new int[length];
        System.out.println("Введите элементы массива:");
        for (int i = 0; i < length; i++) {
            array[i] = scanner.nextInt();
        }
        System.out.println("Массив: " + Arrays.toString(array));
    }
}







class ArrayBubble{
    private long[] a;   //ссылка на массив
    private int elems;  //количество элементов в массиве

    public ArrayBubble(int max){    //конструктор класса
        a = new long[max];          //создание массива размером max
        elems = 0;                  //при создании массив содержит 0 элементов
    }

    public void into(long value){   //метод вставки элемента в массив
        a[elems] = value;           //вставка value в массив a
        elems++;                    //размер массива увеличивается
    }

    public void printer(){          //метод вывода массива в консоль
        for (int i = 0; i < elems; i++){    //для каждого элемента в массиве
            System.out.print(a[i] + " ");   //вывести в консоль
            System.out.println("");         //с новой строки
        }
        System.out.println("----Окончание вывода массива----");
    }

    private void toSwap(int first, int second){ //метод меняет местами пару чисел массива
        long dummy = a[first];      //во временную переменную помещаем первый элемент
        a[first] = a[second];       //на место первого ставим второй элемент
        a[second] = dummy;          //вместо второго элемента пишем первый из временной памяти
    }

    public void bubbleSorter(){     //МЕТОД ПУЗЫРЬКОВОЙ СОРТИРОВКИ
        for (int out = elems - 1; out >= 1; out--){  //Внешний цикл
            for (int in = 0; in < out; in++){       //Внутренний цикл
                if(a[in] > a[in + 1])               //Если порядок элементов нарушен
                    toSwap(in, in + 1);             //вызвать метод, меняющий местами
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        ArrayBubble array = new ArrayBubble(5); //Создаем массив array на 5 элементов

        array.into(163);       //заполняем массив
        array.into(300);
        array.into(184);
        array.into(191);
        array.into(174);

        array.printer();            //выводим элементы до сортировки
        array.bubbleSorter();       //ИСПОЛЬЗУЕМ ПУЗЫРЬКОВУЮ СОРТИРОВКУ
        array.printer();            //снова выводим отсортированный йсписок
    }
}
