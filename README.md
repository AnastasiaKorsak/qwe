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
