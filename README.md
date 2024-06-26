Вот пример кода для вашего приложения:

MainActivity.kt:

```kotlin
import android.content.Intent
import android.os.Bundle
import android.widget.Button
import android.widget.EditText
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val editText1 = findViewById<EditText>(R.id.editText1)
        val editText2 = findViewById<EditText>(R.id.editText2)
        val editText3 = findViewById<EditText>(R.id.editText3)
        val editText4 = findViewById<EditText>(R.id.editText4)
        val editText5 = findViewById<EditText>(R.id.editText5)
        val button = findViewById<Button>(R.id.button)

        button.setOnClickListener {
            val intent = Intent(this, SecondActivity::class.java)
            intent.putExtra("param1", editText1.text.toString())
            intent.putExtra("param2", editText2.text.toString())
            intent.putExtra("param3", editText3.text.toString())
            intent.putExtra("param4", editText4.text.toString())
            intent.putExtra("param5", editText5.text.toString())
            startActivity(intent)
        }
    }
}
```

activity_main.xml:

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/editText1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <EditText
        android:id="@+id/editText2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <EditText
        android:id="@+id/editText3"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <EditText
        android:id="@+id/editText4"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <EditText
        android:id="@+id/editText5"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Submit"/>

</LinearLayout>
```

SecondActivity.kt:

```kotlin
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import kotlinx.android.synthetic.main.activity_second.*
import org.json.JSONObject

class SecondActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_second)

        val param1 = intent.getStringExtra("param1")
        val param2 = intent.getStringExtra("param2")
        val param3 = intent.getStringExtra("param3")
        val param4 = intent.getStringExtra("param4")
        val param5 = intent.getStringExtra("param5")

        val jsonObject = JSONObject()
        jsonObject.put("param1", param1)
        jsonObject.put("param2", param2)
        jsonObject.put("param3", param3)
        jsonObject.put("param4", param4)
        jsonObject.put("param5", param5)

        textView.text = jsonObject.toString()

        backButton.setOnClickListener {
            finish()
        }
    }
}
```

activity_second.xml:

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".SecondActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <Button
        android:id="@+id/backButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Back"/>

</LinearLayout>
```

Не забудьте создать activity_main.xml и activity_second.xml layout файлы и добавить их в папку res/layout вашего проекта.




<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="JSON Conversion Example"
        android:layout_centerInParent="true"
        android:textSize="20sp"/>

</RelativeLayout>






Код активити MainActivity.kt:

```kotlin
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import org.json.JSONObject

data class Entity(val p1: String, val p2: String, val p3: String, val p4: String, val p5: String)

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val entity = Entity("value1", "value2", "value3", "value4", "value5")

        // Конвертировать объект Entity в JSON формат
        val jsonObject = JSONObject()
        jsonObject.put("p1", entity.p1)
        jsonObject.put("p2", entity.p2)
        jsonObject.put("p3", entity.p3)
        jsonObject.put("p4", entity.p4)
        jsonObject.put("p5", entity.p5)
        val json = jsonObject.toString()
        println(json)

        // Конвертировать JSON обратно в объект Entity
        val jsonEntity = JSONObject(json)
        val newEntity = Entity(
            jsonEntity.getString("p1"),
            jsonEntity.getString("p2"),
            jsonEntity.getString("p3"),
            jsonEntity.getString("p4"),
            jsonEntity.getString("p5")
        )
        println(newEntity)
    }
}
```

Не забудьте также создать файл layout с названием activity_main.xml для данной активити.






<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/jsonTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="JSON Output"
        android:textSize="20sp"
        android:layout_marginTop="16dp"
        android:layout_marginStart="16dp"/>

    <TextView
        android:id="@+id/entityTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Entity Output"
        android:textSize="20sp"
        android:layout_marginTop="16dp"
        android:layout_below="@id/jsonTextView"
        android:layout_marginStart="16dp"/>

</RelativeLayout>



import org.json.JSONObject

data class Entity(val p1: String, val p2: String, val p3: String, val p4: String, val p5: String)

fun main() {
    val entity = Entity("value1", "value2", "value3", "value4", "value5")

    // Конвертировать объект Entity в JSON формат
    val jsonObject = JSONObject()
    jsonObject.put("p1", entity.p1)
    jsonObject.put("p2", entity.p2)
    jsonObject.put("p3", entity.p3)
    jsonObject.put("p4", entity.p4)
    jsonObject.put("p5", entity.p5)
    val json = jsonObject.toString()
    println(json)

    // Конвертировать JSON обратно в объект Entity
    val jsonEntity = JSONObject(json)
    val newEntity = Entity(
        jsonEntity.getString("p1"),
        jsonEntity.getString("p2"),
        jsonEntity.getString("p3"),
        jsonEntity.getString("p4"),
        jsonEntity.getString("p5")
    )
    println(newEntity)
}






Sure! Here's an example of a mobile app in Kotlin that includes an entity class with 5 parameters, serializes it to JSON, and deserializes it back to an object from a file:

```kotlin
import com.beust.klaxon.Klaxon
import java.io.File

data class Entity(val p1: String, val p2: String, val p3: String, val p4: String, val p5: String)

fun main() {
    // Creating an instance of the Entity class
    val entity = Entity("value1", "value2", "value3", "value4", "value5")

    // Serializing the entity to JSON
    val json = Klaxon().toJsonString(entity)
    println(json)

    // Writing the JSON to a file
    File("entity.json").writeText(json)

    // Reading the JSON from the file and deserializing it back to an object
    val jsonFromFile = File("entity.json").readText()
    val entityFromFile = Klaxon().parse<Entity>(jsonFromFile)
    
    println(entityFromFile)
}
```

In this code snippet, we define an `Entity` data class with 5 parameters (`p1`, `p2`, `p3`, `p4`, `p5`). We then create an instance of the `Entity` class, serialize it to JSON using the `Klaxon` library, and print the JSON string. We also write the JSON string to a file named `entity.json`.

Next, we read the JSON string from the file, deserialize it back to an `Entity` object, and print the object. This demonstrates how to convert an object to JSON and back using Kotlin and the `Klaxon` library.




import java.util.*;

public class Plane {
    private int id;
    private String name;
    private int year;

    public Plane(int id, String name, int year) {
        this.id = id;
        this.name = name;
        this.year = year;
    }

    public static void main(String[] args) {
        HashSet<Plane> planes = new HashSet<>();
        for (int i = 1; i <= 100; i++) {
            planes.add(new Plane(i, "Plane" + i, 2000 + i));
        }

        Scanner scanner = new Scanner(System.in);
        int choice;
        do {
            System.out.println("Menu:");
            System.out.println("1) Sort by name");
            System.out.println("2) Sort by year of production");
            System.out.println("3) Filter by name");
            System.out.println("4) Filter by year");
            System.out.println("5) Filter by specified year");
            System.out.println("0) Exit");
            choice = scanner.nextInt();
            switch (choice) {
                case 1:
                    List<Plane> sortedByName = new ArrayList<>(planes);
                    Collections.sort(sortedByName, Comparator.comparing(Plane::getName));
                    sortedByName.forEach(System.out::println);
                    break;
                case 2:
                    List<Plane> sortedByYear = new ArrayList<>(planes);
                    Collections.sort(sortedByYear, Comparator.comparingInt(Plane::getYear));
                    sortedByYear.forEach(System.out::println);
                    break;
                case 3:
                    System.out.println("Enter name filter:");
                    String nameFilter = scanner.next();
                    planes.stream()
                          .filter(plane -> plane.getName().contains(nameFilter))
                          .forEach(System.out::println);
                    break;
                case 4:
                    System.out.println("Enter year filter:");
                    int yearFilter = scanner.nextInt();
                    planes.stream()
                          .filter(plane -> plane.getYear() == yearFilter)
                          .forEach(System.out::println);
                    break;
                case 5:
                    System.out.println("Enter specified year:");
                    int specifiedYear = scanner.nextInt();
                    planes.stream()
                          .filter(plane -> plane.getYear() == specifiedYear)
                          .forEach(System.out::println);
                    break;
            }
        } while (choice != 0);
    }

    public String getName() {
        return name;
    }

    public int getYear() {
        return year;
    }

    @Override
    public String toString() {
        return "Plane{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", year=" + year +
                '}';
    }
}







import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Plant {
    private int id;
    private String name;
    private String description;
    private long harvestTime;

    public Plant(int id, String name, String description, long harvestTime) {
        this.id = id;
        this.name = name;
        this.description = description;
        this.harvestTime = harvestTime;
    }

    public String toString() {
        return "ID: " + id + ", Name: " + name + ", Description: " + description + ", Harvest Time: " + harvestTime;
    }
}

public class GardenerApp {
    private static List<Plant> plants = new ArrayList<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("Gardener Menu:");
            System.out.println("1. View Plants");
            System.out.println("2. Add Plant");
            System.out.println("3. Exit");

            int choice = scanner.nextInt();

            switch(choice) {
                case 1:
                    viewPlants();
                    break;
                case 2:
                    addPlant();
                    break;
                case 3:
                    System.out.println("Exiting program");
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }

    private static void viewPlants() {
        if (plants.isEmpty()) {
            System.out.println("No plants in the garden.");
        } else {
            for (Plant plant : plants) {
                System.out.println(plant);
            }
        }
    }

    private static void addPlant() {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Enter plant ID:");
        int id = scanner.nextInt();
        scanner.nextLine(); // Consume newline

        System.out.println("Enter plant name:");
        String name = scanner.nextLine();

        System.out.println("Enter plant description:");
        String description = scanner.nextLine();

        System.out.println("Enter harvest time:");
        long harvestTime = scanner.nextLong();

        Plant newPlant = new Plant(id, name, description, harvestTime);
        plants.add(newPlant);

        System.out.println("Plant added successfully.");
    }
}






import java.util.ArrayList;

class Food {
    private int id;
    private String name;
    private String description;

    public Food(int id, String name, String description) {
        this.id = id;
        this.name = name;
        this.description = description;
    }

    // Getters and Setters
}

public class FoodDataStructure {
    private ArrayList<Food> foods = new ArrayList<>();

    public void addFood(Food food) {
        foods.add(food);
    }

    public void addFirst(Food food) {
        foods.add(0, food);
    }

    public void addMiddle(Food food) {
        foods.add(foods.size() / 2, food);
    }

    public void addLast(Food food) {
        foods.add(food);
    }

    public void removeFood(Food food) {
        foods.remove(food);
    }

    public void modifyFirst(Food food) {
        foods.set(0, food);
    }

    public void modifyMiddle(Food food) {
        foods.set(foods.size() / 2, food);
    }

    public void modifyLast(Food food) {
        foods.set(foods.size() - 1, food);
    }

    public static void main(String[] args) {
        FoodDataStructure foodDS = new FoodDataStructure();
        long startTime, endTime, totalTime;

        // Create and add 100000 entities
        for (int i = 0; i < 100000; i++) {
            Food food = new Food(i, "Food" + i, "Description" + i);
            foodDS.addFood(food);
        }

        // Test addFirst method
        Food newFood1 = new Food(100001, "New Food First", "New Description First");
        startTime = System.currentTimeMillis();
        foodDS.addFirst(newFood1);
        endTime = System.currentTimeMillis();
        totalTime = endTime - startTime;
        System.out.println("Add First method time: " + totalTime + "ms");

        // Test addMiddle method
        Food newFood2 = new Food(100002, "New Food Middle", "New Description Middle");
        startTime = System.currentTimeMillis();
        foodDS.addMiddle(newFood2);
        endTime = System.currentTimeMillis();
        totalTime = endTime - startTime;
        System.out.println("Add Middle method time: " + totalTime + "ms");

        // Test addLast method
        Food newFood3 = new Food(100003, "New Food Last", "New Description Last");
        startTime = System.currentTimeMillis();
        foodDS.addLast(newFood3);
        endTime = System.currentTimeMillis();
        totalTime = endTime - startTime;
        System.out.println("Add Last method time: " + totalTime + "ms");

        // Test removeFood method
        startTime = System.currentTimeMillis();
        foodDS.removeFood(newFood1);
        endTime = System.currentTimeMillis();
        totalTime = endTime - startTime;
        System.out.println("Remove method time: " + totalTime + "ms");

        // Test modifyFirst method
        Food modifiedFood1 = new Food(100001, "Modified Food First", "Modified Description First");
        startTime = System.currentTimeMillis();
        foodDS.modifyFirst(modifiedFood1);
        endTime = System.currentTimeMillis();
        totalTime = endTime - startTime;
        System.out.println("Modify First method time: " + totalTime + "ms");

        // Test modifyMiddle method
        Food modifiedFood2 = new Food(50000, "Modified Food Middle", "Modified Description Middle");
        startTime = System.currentTimeMillis();
        foodDS.modifyMiddle(modifiedFood2);
        endTime = System.currentTimeMillis();
        totalTime = endTime - startTime;
        System.out.println("Modify Middle method time: " + totalTime + "ms");

        // Test modifyLast method
        Food modifiedFood3 = new Food(100003, "Modified Food Last", "Modified Description Last");
        startTime = System.currentTimeMillis();
        foodDS.modifyLast(modifiedFood3);
        endTime = System.currentTimeMillis();
        totalTime = endTime - startTime;
        System.out.println("Modify Last method time: " + totalTime + "ms");
    }
}






import java.util.Scanner;
import java.util.ArrayList;

class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<String> books = new ArrayList<>();

        while (true) {
            System.out.println("1. Посчитать все книги");
            System.out.println("2. Добавить книгу");
            System.out.println("3. Удалить книгу");
            System.out.println("4. Выйти");

            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.println("Общее количество книг: " + books.size());
                    break;
                case 2:
                    System.out.print("Введите название книги: ");
                    String newBook = scanner.next();
                    books.add(newBook);
                    System.out.println("Книга добавлена");
                    break;
                case 3:
                    System.out.print("Введите номер книги для удаления: ");
                    int bookIndex = scanner.nextInt();
                    if (bookIndex >= 0 && bookIndex < books.size()) {
                        String removedBook = books.remove(bookIndex);
                        System.out.println("Книга " + removedBook + " удалена");
                    } else {
                        System.out.println("Книги с таким номером не существует");
                    }
                    break;
                case 4:
                    System.out.println("Выход из программы");
                    System.exit(0);
                    break;
                default:
                    System.out.println("Некорректный выбор");
            }
        }
    }
}







import java.util.Scanner;

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
}






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
