Процесс выполнения Java-Spring-приложения.

# Gradle

1) Gradle: Запускается `build.gradle`.
Загрузка плагинов `spring-boot` `java`. Разбирает `dependencies`. Инкрементная сборка.
Создаётся `Task Graph`.
	Ключевые слова в `dependencies`:

| Ключевое слово        | Что делает                                                                                                         |
| --------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `implementation`      | Добавляет зависимость **для компиляции и выполнения**. Видна только внутри модуля. **Рекомендуется по умолчанию**. |
| `compileOnly`         | Только **для компиляции**, **не будет в JAR**. Часто используется с Lombok.                                        |
| `runtimeOnly`         | Зависимость **только для запуска**, не нужна на этапе компиляции. Например, JDBC-драйвер.                          |
| `annotationProcessor` | Используется **аннотационными процессорами**, как Lombok, MapStruct.                                               |
| `testImplementation`  | Зависимость для **тестов** (JUnit, Mockito и пр.).                                                                 |
| `testRuntimeOnly`     | Только для **запуска тестов**. Например, драйвер базы данных.                                                      |

2) Компиляция Java-кода.
Вызывается `javac` компилирует классы из `.java` в `.class` и помещает их в `build`.
`Javac` - это сам компилятор. A `Java` - интерпретатор, для запуска байт-кода `.class`.
То есть:
```bash
javac MyApp.java
java MyApp
```
На этом же шаге обрабатываются аннотации (например, @Service, Lombok).

3) `processResources` (cборка ресурсов).
Копируется `src/main/resources...` в `build/resources...`.

4) Сборка **`Jar`** (`bootJar`).
Через плагин `Spring boot` выполняется `bootJar`.
Он собирает все `.class` файлы, ресурсы, зависимости в один большой `.jar`, который лежит внутри `build/libs/name.jar`

5) Запуск `bootRun`.
`BootRun` запускает класс(спринга-boot) `JarLauncher`. `ClassLoader` загружает зависимости.
Запускается главная функция `main()` из `@SpringBootApplication`.


Команды:
`Ctr+Shift+O` - пере-сборка Gradle.
`./gradlew --refresh-dependencies` - синхронизация зависимостей (пере-сборка Gradle).

`./gradlew bootJar` - создание `jar`-инка. 
`./gradlew clean build` - очистка + пересборка.

`./gradlew bootJar taskTree` - для создания дерева зависимостей задач. Нужен плагин: `id "com.dorongold.task-tree" version "4.0.1"`.

