public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}

1. В stack memory создан фрейм main. Во фрейме main создается int переменная "i".
2. Загрузка класса Object (Bootstrap Classloader). В куче создается объект типа Object, а ссылка на этот объект в main frame .
3. Загрузка класса Integer (Bootstrap Classloader). Во фрейм main помещается имя переменной(ii) и ссылка на объект, который находится в куче.
4. В stack memory создается новый фрейм printAll с переменными о, i, ii.
5. Во фрейм printAll помещается имя переменной uselessVar и ссылка на объект в куче.
6. Создается фрейм out.println, в него передаются ссылки переменных "o", "i", "ii". Также создается фрейм toString для этих переменных. Ссылка на созданную строку передается в стэк,а строка - в кучу. Удаление фрейма println.
7. В куче создается объект со значением "finished", создается фрейм out.println со ссылкой
   на это объект. Завершение программы, очистка стека и кучи сборщиком мусора.