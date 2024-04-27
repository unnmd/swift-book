# Тур по Swift

Изучите особенности и синтаксис Swift.

По традиции, первая программа на новом языке 
должна выводить слова "Hello, world!" на экран. 
В Swift это можно сделать всего одной строкой:

<!--
  K&R использует "hello, world".
  Кажется, стоит нарушить традицию и использовать правильный регистр букв.
-->

```swift
print("Hello, world!")
// Выводит "Hello, world!"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> print("Hello, world!")
  <- Hello, world!
  ```
-->

Синтаксис этой строки должен быть вам знаком, если вы знакомы с другими языками 
программирования. В Swift эта строка кода представляет собой полную программу. 
Вам не нужно импортировать отдельную библиотеку для функций, 
таких как вывод текста или обработка строк. 
Код, написанный на глобальном уровне, используется 
в качестве точки входа в программу, 
поэтому вам не нужна функция `main()`. 
Также вам не нужно ставить точки с запятой 
в конце каждого оператора.

Этот тур предоставит вам достаточно информации, 
чтобы начать писать код на Swift, 
показывая, как выполнять различные программные задачи. 
Не беспокойтесь, если что-то не понятно — 
все введенное в этом туре 
подробно объяснено в остальной части этой книги.

## Простые значения

Используйте `let` для создания константы и `var` для создания переменной.
Знначение константы 
необязательно знать во время компиляции,
но вы должны присвоить ей значение ровно один раз.
Это означает, что вы можете использовать константы для обозначения значения,
которое определяется один раз, но используется во многих местах.

```swift
var myVariable = 42
myVariable = 50
let myConstant = 42
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var myVariable = 42
  -> myVariable = 50
  -> let myConstant = 42
  ```
-->

Константа или переменная должна иметь тот же тип, что и значение, 
которое вы хотите ей присвоить. 
Однако вам не всегда нужно явно указывать тип. 
Предоставление значения при создании константы или переменной позволяет 
компилятору вывести ее тип. 
В приведенном выше примере компилятор выводит, 
что `myVariable` является целым числом, потому что его начальное значение — 
это целое число.

Если начальное значение не предоставляет достаточно 
информации (или его вообще нет),
укажите тип, написав его после переменной, 
разделяя двоеточием.

```swift
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let implicitInteger = 70
  -> let implicitDouble = 70.0
  -> let explicitDouble: Double = 70
  ```
-->

> Эксперимент: Создайте константу с 
> явным типом `Float` и значением `4`.

Значения никогда не неявно преобразуются в другой тип. 
Если вам нужно преобразовать значение в другой тип, 
явно создайте экземпляр нужного типа.

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let label = "The width is "
  -> let width = 94
  -> let widthLabel = label + String(width)
  >> print(widthLabel)
  << The width is 94
  ```
-->

> Эксперимент: Попробуйте удалить преобразование в `String` из последней строки.
> Какую ошибку вы получите?

<!--
  ЗАДАЧА: Обсудить с основными авторами ---
  помогают ли вам эти эксперименты, которые знакомят вас с ошибками,
  изучать что-то?
-->

Есть еще более простой способ поместить значение в строку: 
напишите значение в круглых скобках 
и поставьте обратный слэш (`\`) перед скобками. 
Например:

```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let apples = 3
  -> let oranges = 5
  -> let appleSummary = "I have \(apples) apples."
  >> print(appleSummary)
  << I have 3 apples.
  -> let fruitSummary = "I have \(apples + oranges) pieces of fruit."
  >> print(fruitSummary)
  << I have 8 pieces of fruit.
  ```
-->

> Эксперимент: Используйте `\()` чтобы добавить вычисления 
> с плавающей запятой в строку и 
> для включения имени в приветствие.

Используйте три двойные кавычки (`"""`) для строк, 
которые занимают несколько строк. 
Отступ в начале каждой закавыченной строки удаляется, 
если он совпадает с отступом закрывающих кавычек. 
Например:

```swift
let quotation = """
        Даже если слева есть пробел,
        фактические строки не отступлены.
            Кроме этой строки.
        Двойные кавычки (") могут появляться без экранирования.

        У меня все еще есть \(apples + oranges) кусочков фруктов.
        """
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let quotation = """
     I said "I have \(apples) apples."
     And then I said "I have \(apples + oranges) pieces of fruit."
     """
  ```
-->

<!--
  Невозможно показать пример отступа в вышеуказанной строке с тройными кавычками.
  <rdar://problem/49129068> Форматирование кода Swift повреждает отступление
-->

Создавайте массивы и словари с использованием квадратных скобок (`[]`) 
и обращайтесь к их элементам, 
указывая индекс или ключ в скобках. 
Запятая разрешена после последнего элемента.

<!--
  ОТСЫЛКА
  Список фруктов взят из цветов, в которых выпускался первоначальный iMac,
  следуя за начальным запуском iMac в цвете Bondi Blue, упорядоченном по SKU -
  что также совпадает с порядком их появления в рекламе:

       M7389LL/A (266 МГц Strawberry)
       M7392LL/A (266 МГц Lime)
       M7391LL/A (266 МГц Tangerine)
       M7390LL/A (266 МГц Grape)
       M7345LL/A (266 МГц Blueberry)

       M7441LL/A (333 МГц Strawberry)
       M7444LL/A (333 МГц Lime)
       M7443LL/A (333 МГц Tangerine)
       M7442LL/A (333 МГц Grape)
       M7440LL/A (333 МГц Blueberry)
-->

<!--
  ОТСЫЛКА
  "Профессии" - это отсылка к сериалу "Firefly",
  конкретно к шутке Мэла о работе Джейна на корабле.

  Не могу найти конкретной серии,
  но она встречается в нескольких списках лучших цитат из "Firefly":

  Мэл: Джейн, ты будешь вести себя прилично, или я зашью тебе рот.
       Мы поняли друг друга?
  Джейн: Ты не платишь мне за красивые слова. [...]
  Мэл: Уходи от этого стола. Прямо сейчас.
  [Джейн берет еду и уходит]
    Саймон: За что ему платят?
    Мэл: Что?
    Саймон: Мне просто интересно, чем он занимается на корабле.
    Мэл: За пиар.
-->

```swift
var fruits = ["клубника", "лимоны", "мандарины"]
fruits[1] = "виноград"

var occupations = [
    "Малкольм": "Капитан",
    "Кейли": "Механик",
 ]
occupations["Джейн"] = "Отношения с общественностью"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var fruits = ["strawberries", "limes", "tangerines"]
  -> fruits[1] = "grapes"
  ---
  -> var occupations = [
         "Malcolm": "Captain",
         "Kaylee": "Mechanic",
      ]
  -> occupations["Jayne"] = "Public Relations"
  ```
-->

<!-- Apple Books screenshot begins here. -->

Массивы автоматически увеличиваются при добавлении элементов.

```swift
fruits.append("голубика")
print(fruits)
// Выводит "["клубника", "виноград", "мандарины", "голубика"]"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> fruits.append("blueberries")
  -> print(fruits)
  <- ["strawberries", "grapes", "tangerines", "blueberries"]
  ```
-->

Вы также используете скобки для создания пустого массива или словаря. 
Для массива напишите `[]`, 
а для словаря напишите `[:]`.

```swift
fruits = []
occupations = [:]
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> fruits = []
  -> occupations = [:]
  ```
-->

Если вы присваиваете пустой массив или словарь новой переменной 
или другому месту, где нет информации о типе, 
вы должны указать тип.

```swift
let emptyArray: [String] = []
let emptyDictionary: [String: Float] = [:]
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let emptyArray: [String] = []
  -> let emptyDictionary: [String: Float] = [:]
  ---
  -> let anotherEmptyArray = [String]()
  -> let emptyDictionary = [String: Float]()
  ```
-->

## Управление потоком

Используйте `if` и `switch` для создания условий, 
а также `for`-`in`, `while` и `repeat`-`while` 
для создания циклов. 
Круглые скобки вокруг условия или переменной цикла необязательны. 
Фигурные скобки вокруг тела обязательны.

```swift
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
print(teamScore)
// Выводит "11"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let individualScores = [75, 43, 103, 87, 12]
  -> var teamScore = 0
  -> for score in individualScores {
         if score > 50 {
             teamScore += 3
         } else {
             teamScore += 1
         }
     }
  -> print(teamScore)
  <- 11
  ```
-->

<!--
  ОТСЫЛКА
  Жевательные медвежонки - это сладость, тесно связанная
  с предыдущими воплощениями Доктора в Докторе Кто.
-->

<!--
let haveJellyBabies = true
if haveJellyBabies {
}
<< Желаете ли вы жевательного медвежонка?
-->

В операторе `if` условие 
должно быть логическим выражением. 
Это означает, что код, такой как `if score { ... }`, вызовет ошибку, 
а не неявное сравнение с нулем.

Вы можете использовать `if` или `switch` 
после знака равенства (`=`) при присвоении 
или после `return`, 
чтобы выбрать значение на основе условия.

```swift
let scoreDecoration = if teamScore > 10 {
    "🎉"
} else {
    ""
}
print("Score:", teamScore, scoreDecoration)
// Выводит "Score: 11 🎉"
```

Вы можете использовать `if` и `let` вместе 
для работы с значениями, которые могут отсутствовать. 
Эти значения представлены в виде опционалов. 
Опциональное значение может содержать значение 
или `nil`, чтобы указать, что значение отсутствует. 
Поставьте вопросительный знак (`?`) после типа значения, 
чтобы пометить его как опциональное.

<!-- Apple Books screenshot ends here. -->

<!--
  ОТСЫЛКА
  Джон Эпплсид - это вымышленное имя, используемое Apple,
  прослеживаемое, по крайней мере, до базы данных контактов,
  которая поставляется с SDK в симуляторе.
-->

```swift
var optionalString: String? = "Hello"
print(optionalString == nil)
// Выводит "false"

var optionalName: String? = "Джон Эпплсид"
var greeting = "Привет!"
if let name = optionalName {
    greeting = "Привет, \(name)"
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var optionalString: String? = "Hello"
  -> print(optionalString == nil)
  <- false
  ---
  -> var optionalName: String? = "John Appleseed"
  -> var greeting = "Hello!"
  -> if let name = optionalName {
         greeting = "Hello, \(name)"
     }
  >> print(greeting)
  << Hello, John Appleseed
  ```
-->

> ЭКСПЕРИМЕНТ: Измените `optionalName` на `nil`.
> Какое приветствие вы получите?
> Добавьте блок `else`, который устанавливает другое приветствие,
> если `optionalName` равно `nil`.

Если опциональное значение равно `nil`, 
условие будет ложным, и код в фигурных скобках будет пропущен. 
В противном случае опциональное значение разворачивается и 
присваивается константе после `let`, 
что делает разворачиваемое значение доступным 
внутри блока кода.

Другой способ работы с опциональными значениями — 
предоставление значения по умолчанию с использованием оператора `??`. 
Если опциональное значение отсутствует, 
вместо него используется значение по умолчанию.

```swift
let nickname: String? = nil
let fullName: String = "Джон Эпплсид"
let informalGreeting = "Привет \(nickname ?? fullName)"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let nickname: String? = nil
  -> let fullName: String = "John Appleseed"
  -> let informalGreeting = "Hi \(nickname ?? fullName)"
  >> print(informalGreeting)
  << Hi John Appleseed
  ```
-->

Вы можете использовать более короткую запись для разворачивания значения, 
используя тот же самый тип для этого разворачиваемого значения.

```swift
if let nickname {
    print("Привет, \(nickname)")
}
// Ничего не выводит, потому что nickname равно nil.
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> if let nickname {
         print("Hey, \(nickname)")
     }
  ```
-->

`Switch` поддерживает любой тип данных 
и множество операций сравнения — 
он не ограничен целыми числами 
и проверками на равенство.

<!--
  ОТСЫЛКА
  Овощи и продукты из овощей
  были всего лишь удобным выбором для оператора switch.
  У них есть различные свойства
  и подходят к яблокам и апельсинам, использованным в предыдущем примере.
-->

```swift
let vegetable = "красный перец"
switch vegetable {
case "сельдерей":
    print("Добавьте немного изюма и получите муравьев на бревне.")
case "огурец", "водосквоз":
    print("Это был бы хороший чайный бутерброд.")
case let x where x.hasSuffix("перец"):
    print("Это острый \(x)?")
default:
    print("Все вкусно в супе.")
}
// Выводит "Это острый красный перец?"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let vegetable = "red pepper"
  -> switch vegetable {
         case "celery":
             print("Add some raisins and make ants on a log.")
         case "cucumber", "watercress":
             print("That would make a good tea sandwich.")
         case let x where x.hasSuffix("pepper"):
             print("Is it a spicy \(x)?")
         default:
             print("Everything tastes good in soup.")
     }
  <- Is it a spicy red pepper?
  ```
-->

> Эксперимент: Попробуйте удалить блок по умолчанию.
> Какую ошибку вы получите?

Обратите внимание, как `let` можно использовать в шаблоне
для присвоения значения, которое соответствует шаблону,
константе.

После выполнения кода внутри блока `switch`, который соответствует,
программа выходит из оператора `switch`.
Выполнение не продолжается на следующий случай,
поэтому вам не нужно явно выходить из оператора `switch`
в конце кода каждого случая.

<!--
  Пропускаем упоминание ключевого слова "fallthrough".
  Это есть в руководстве/справочнике, если вам это нужно.
-->

Вы используете `for`-`in` для итерации по элементам словаря,
предоставляя пару имен для использования
для каждой пары ключ-значение.
Словари являются неупорядоченной коллекцией,
поэтому их ключи и значения итерируются
в произвольном порядке.

<!--
  ОТСЫЛКА
  Простые, квадратные и числа Фибоначчи
  - это всего лишь удобные наборы чисел,
  с которыми многие разработчики уже знакомы,
  и их можно использовать для простых математических операций.
-->

```swift
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (_, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)
// Выводит "25"
```

<!--
  - тест: `guided-tour`

  ```swifttest
  -> let interestingNumbers = [
         "Prime": [2, 3, 5, 7, 11, 13],
         "Fibonacci": [1, 1, 2, 3, 5, 8],
         "Square": [1, 4, 9, 16, 25],
     ]
  -> var largest = 0
  -> for (_, numbers) in interestingNumbers {
         for number in numbers {
             if number > largest {
                 largest = number
             }
         }
     }
  -> print(largest)
  <- 25
  ```
-->

> Эксперимент: Замените `_` на имя переменной,
> и отслеживайте, какой тип числа был наибольшим.

Используйте `while` для повторения блока кода до изменения условия.
Условие цикла может быть расположено в конце,
что гарантирует, что цикл выполняется как минимум один раз.

<!--
  ОТСЫЛКА
  Этот пример довольно каркасный - m и n довольно скучные.
  Мне не удалось придумать что-то достаточно интересное на тот момент,
  поэтому я просто использовал это.
-->

```swift
var n = 2
while n < 100 {
    n *= 2
}
print(n)
// Выводит "128"

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
// Выводит "128"
```

<!--
  - тест: `guided-tour`

  ```swifttest
  -> var n = 2
  -> while n < 100 {
         n *= 2
     }
  -> print(n)
  <- 128
  ---
  -> var m = 2
  -> repeat {
         m *= 2
     } while m < 100
  -> print(m)
  <- 128
  ```
-->

> Эксперимент:
> Измените условие с `m < 100` на `m < 0`
> чтобы увидеть, как по-разному себя ведут `while` и `repeat`-`while`,
> когда условие цикла уже является ложным.

Вы можете хранить индекс в цикле,
используя `..<` для создания диапазона индексов.

```swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
// Выводит "6"
```

<!--
  - тест: `guided-tour`

  ```swifttest
  -> var total = 0
  -> for i in 0..<4 {
         total += i
     }
  -> print(total)
  <- 6
  ```
-->

Используйте `..<` для создания диапазона, который исключает его верхнее значение,
и используйте `...` для создания диапазона, который включает оба значения.

## Функции и Замыкания

Используйте `func` для объявления функции.
Вызывайте функцию, следуя ее имени
списком аргументов в круглых скобках.
Используйте `->` для разделения имен параметров и их типов
от типа возврата функции.

<!--
  ОТСЫЛКА
  Bob используется как просто общее имя,
  но также как ссылка на отца Алекса.
  Вторник используется с предположением, что многие люди будут читать 
  во вторник после ключевого доклада WWDC.
-->

```swift
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```

<!--
  - тест: `guided-tour`

  ```swifttest
  -> func greet(person: String, day: String) -> String {
         return "Hello \(person), today is \(day)."
     }
  >> let greetBob =
  -> greet(person: "Bob", day: "Tuesday")
  >> print(greetBob)
  << Hello Bob, today is Tuesday.
  ```
-->

> Эксперимент: Удалите параметр `day`.
> Добавьте параметр для включения сегодняшнего обеденного спецпредложения.

По умолчанию
функции используют имена своих параметров
в качестве меток для своих аргументов.
Записывайте пользовательскую метку аргумента перед именем параметра,
или используйте `_`, чтобы не использовать метку аргумента.

```swift
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func greet(_ person: String, on day: String) -> String {
         return "Hello \(person), today is \(day)."
     }
  >> let greetJohn =
  -> greet("John", on: "Wednesday")
  >> print(greetJohn)
  << Hello John, today is Wednesday.
  ```
-->

Используйте кортеж для создания составного значения ---
например, для возвращения нескольких значений из функции.
Элементы кортежа могут быть обращены
как по имени, так и по номеру.

<!--
  ОТСЫЛКА
  min, max и sum удобны для этого примера,
  потому что они все являются простыми операциями,
  выполняемыми над одним и тем же типом данных.
  Это дает функции причину возвращать кортеж.
-->

```swift
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0

    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }

    return (min, max, sum)
}
let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
print(statistics.sum)
// Выводит "120"
print(statistics.2)
// Выводит "120"
```

<!--
  - тест: `guided-tour`

  ```swifttest
  -> func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
         var min = scores[0]
         var max = scores[0]
         var sum = 0

         for score in scores {
             if score > max {
                 max = score
             } else if score < min {
                 min = score
             }
             sum += score
         }

         return (min, max, sum)
     }
  -> let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
  >> print(statistics)
  << (min: 3, max: 100, sum: 120)
  -> print(statistics.sum)
  <- 120
  -> print(statistics.2)
  <- 120
  ```
-->

Функции могут быть вложенными.
Вложенные функции имеют доступ к переменным,
которые были объявлены во внешней функции.
Вы можете использовать вложенные функции,
чтобы организовать код в функции,
которая является длинной или сложной.

```swift
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```

<!--
  - тест: `guided-tour`

  ```swifttest
  -> func returnFifteen() -> Int {
         var y = 10
         func add() {
             y += 5
         }
         add()
         return y
     }
  >> let fifteen =
  -> returnFifteen()
  >> print(fifteen)
  << 15
  ```
-->

Функции - это тип первого класса.
Это означает, что функция может возвращать другую функцию в качестве своего значения.

```swift
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```

<!--
  - тест: `guided-tour`

  ```swifttest
  -> func makeIncrementer() -> ((Int) -> Int) {
         func addOne(number: Int) -> Int {
             return 1 + number
         }
         return addOne
     }
  -> var increment = makeIncrementer()
  >> let incrementResult =
  -> increment(7)
  >> print(incrementResult)
  << 8
  ```
-->

Функция может принимать другую функцию в качестве одного из своих аргументов.

```swift
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)
```

<!--
  - тест: `guided-tour`

  ```swifttest
  -> func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
         for item in list {
             if condition(item) {
                 return true
             }
         }
         return false
     }
  -> func lessThanTen(number: Int) -> Bool {
         return number < 10
     }
  -> var numbers = [20, 19, 7, 12]
  >> let anyMatches =
  -> hasAnyMatches(list: numbers, condition: lessThanTen)
  >> print(anyMatches)
  << true
  ```
-->

Функции на самом деле представляют собой особый случай замыканий:
блоки кода, которые можно вызвать позже.
Код в замыкании имеет доступ к таким вещам, как переменные и функции,
которые были доступны в области видимости, где было создано замыкание,
даже если замыкание находится в другой области видимости, когда оно выполняется ---
вы уже видели пример этого с вложенными функциями.
Вы можете написать замыкание без имени,
обрамив код фигурными скобками (`{}`).
Используйте `in` для разделения аргументов и типа возвращаемого значения от тела.

```swift
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```

<!--
  - test: `guided-tour`

  ```swifttest
  >> let numbersMap =
  -> numbers.map({ (number: Int) -> Int in
         let result = 3 * number
         return result
     })
  >> print(numbersMap)
  << [60, 57, 21, 36]
  ```
-->

> Эксперимент: Перепишите замыкание так, чтобы оно возвращало ноль для всех нечетных чисел.

У вас есть несколько вариантов написания замыканий более кратко.
Когда тип замыкания уже известен,
например, при обратном вызове делегата,
вы можете опустить тип его параметров,
его тип возвращаемого значения или оба.
Замыкания с одним оператором неявно возвращают значение
их единственного оператора.

```swift
let mappedNumbers = numbers.map({ number in 3 * number })
print(mappedNumbers)
// Выводит "[60, 57, 21, 36]"
```

<!--
  - тест: `guided-tour`

  ```swifttest
  -> let mappedNumbers = numbers.map({ number in 3 * number })
  -> print(mappedNumbers)
  <- [60, 57, 21, 36]
  ```
-->

Вы можете обращаться к параметрам по номеру, а не по имени ---
этот подход особенно полезен в очень коротких замыканиях.
Замыкание, передаваемое в качестве последнего аргумента функции,
может следовать сразу после скобок.
Когда замыкание - единственный аргумент функции,
вы можете полностью опустить скобки.

```swift
let sortedNumbers = numbers.sorted { $0 > $1 }
print(sortedNumbers)
// Выводит "[20, 19, 12, 7]"
```

<!--
  - тест: `guided-tour`

  ```swifttest
  -> let sortedNumbers = numbers.sorted { $0 > $1 }
  -> print(sortedNumbers)
  <- [20, 19, 12, 7]
  ```
-->

<!--
  Вызвана функция sorted() для переменной, а не литерала, чтобы обойти проблему в Xcode. См. <rdar://17540974>.
-->

<!--
  Пропущен sort(foo, <), потому что это часто вызывает ложные предупреждения в Xcode. См. <rdar://17047529>.
-->

<!--
  Пропущены пользовательские операторы как "продвинутые" темы.
-->

## Объекты и классы

Используйте `class`, за которым следует имя класса, чтобы создать класс.
Объявление свойства в классе записывается так же,
как объявление константы или переменной,
за исключением того, что оно находится в контексте класса.
Точно так же записываются методы и функции.

<!--
  ОТСЫЛКА
  Формы используются в качестве примера объекта,
  потому что они знакомы и имеют понятие свойств
  и наследования/подкатегоризации.
  Они не являются идеальным вариантом —
  возможно, их лучше было бы моделировать как структуры —,
  но это не позволило бы им наследовать поведение.
-->

```swift
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "Фигура с \(numberOfSides) сторонами."
    }
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class Shape {
         var numberOfSides = 0
         func simpleDescription() -> String {
             return "Фигура с \(numberOfSides) сторонами."
         }
     }
  >> print(Shape().simpleDescription())
  << Фигура с 0 сторонами.
  ```
-->

> Эксперимент: Добавьте константное свойство с `let`,
> и добавьте еще один метод, который принимает аргумент.

Создайте экземпляр класса,
поставив скобки после имени класса.
Используйте синтаксис точечной нотации для доступа
к свойствам и методам экземпляра.

```swift
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var shape = Shape()
  -> shape.numberOfSides = 7
  -> var shapeDescription = shape.simpleDescription()
  >> print(shapeDescription)
  << Фигура с 7 сторонами.
  ```
-->

В этой версии класса `Shape` чего-то важного не хватает:
инициализатора для настройки класса при создании экземпляра.
Используйте `init`, чтобы создать его.

```swift
class NamedShape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
       self.name = name
    }

    func simpleDescription() -> String {
       return "Фигура с \(numberOfSides) сторонами."
    }
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class NamedShape {
         var numberOfSides: Int = 0
         var name: String
  ---
         init(name: String) {
            self.name = name
         }
  ---
         func simpleDescription() -> String {
            return "Фигура с \(numberOfSides) сторонами."
         }
     }
  >> print(NamedShape(name: "тестовое имя").name)
  << тестовое имя
  >> print(NamedShape(name: "тестовое имя").simpleDescription())
  << Фигура с 0 сторонами.
  ```
-->

Обратите внимание, как используется `self`,
чтобы отличить свойство `name`
от аргумента `name` инициализатора.
Аргументы инициализатора передаются как при вызове функции
при создании экземпляра класса.
Каждому свойству нужно присвоить значение ---
либо в его объявлении (как с `numberOfSides`),
либо в инициализаторе (как с `name`).

Используйте `deinit`, чтобы создать деинициализатор,
если вам нужно выполнить некоторые действия перед освобождением памяти объекта.

Подклассы включают имя своего суперкласса
после своего собственного имени класса,
разделенные двоеточием.
Нет требования, чтобы классы подклассировали какой-либо стандартный корневой класс,
поэтому вы можете включать или опускать суперкласс по мере необходимости.

Методы в подклассе, переопределяющие реализацию суперкласса,
помечаются ключевым словом `override` ---
переопределение метода случайно, без `override`,
обнаруживается компилятором как ошибка.
Компилятор также обнаруживает методы с `override`,
которые фактически не переопределяют ни один метод в суперклассе.

```swift
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() -> Double {
        return sideLength * sideLength
    }

    override func simpleDescription() -> String {
        return "Квадрат со стороной длиной \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "мой тестовый квадрат")
test.area()
test.simpleDescription()
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class Square: NamedShape {
         var sideLength: Double
  ---
         init(sideLength: Double, name: String) {
             self.sideLength = sideLength
             super.init(name: name)
             numberOfSides = 4
         }
  ---
         func area() -> Double {
             return sideLength * sideLength
         }
  ---
         override func simpleDescription() -> String {
             return "Квадрат со стороной длиной \(sideLength)."
         }
     }
  -> let test = Square(sideLength: 5.2, name: "мой тестовый квадрат")
  >> let testArea =
  -> test.area()
  >> print(testArea)
  << 27.040000000000003
  >> let testDesc =
  -> test.simpleDescription()
  >> print(testDesc)
  << Квадрат со стороной длиной 5.2.
  ```
-->

> Эксперимент: Создайте еще один подкласс `NamedShape`
> с именем `Circle`
> принимающий радиус и имя
> в качестве аргументов для инициализатора.
> Реализуйте методы `area()` и `simpleDescription()`
> в классе `Circle`.

В дополнение к простым свойствам, которые хранятся,
свойства могут иметь геттер и сеттер.

```swift
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }

    var perimeter: Double {
        get {
             return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }

    override func simpleDescription() -> String {
        return "Равносторонний треугольник со стороной длиной \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "треугольник")
print(triangle.perimeter)
// Выводит "9.3"
triangle.perimeter = 9.9
print(triangle.sideLength)
// Выводит "3.3000000000000003"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class EquilateralTriangle: NamedShape {
         var sideLength: Double = 0.0
  ---
         init(sideLength: Double, name: String) {
             self.sideLength = sideLength
             super.init(name: name)
             numberOfSides = 3
         }
  ---
         var perimeter: Double {
             get {
                  return 3.0 * sideLength
             }
             set {
                 sideLength = newValue / 3.0
             }
         }
  ---
         override func simpleDescription() -> String {
             return "An equilateral triangle with sides of length \(sideLength)."
         }
     }
  -> var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
  -> print(triangle.perimeter)
  <- 9.3
  -> triangle.perimeter = 9.9
  -> print(triangle.sideLength)
  <- 3.3000000000000003
  ```
-->

В сеттере для `perimeter` новое значение имеет неявное имя `newValue`.
Вы можете предоставить явное имя в скобках после `set`.

Обратите внимание, что инициализатор для класса `EquilateralTriangle`
имеет три разных шага:

1. Установка значения свойств, объявленных подклассом.
2. Вызов инициализатора суперкласса.
3. Изменение значения свойств, определенных суперклассом.
   Любая дополнительная настройка, использующая методы, геттеры или сеттеры,
   также может быть выполнена в этот момент.

Если вам не нужно вычислять свойство,
но вам все равно нужно предоставить код,
который выполняется перед и после установки нового значения,
используйте `willSet` и `didSet`.
Предоставленный вами код выполняется каждый раз, когда значение изменяется вне инициализатора.
Например, в приведенном ниже классе
гарантируется, что длина стороны его треугольника
всегда равна длине стороны его квадрата.

<!--
  Этот пример с треугольником и квадратом можно улучшить.
  Цель состоит в том, чтобы показать, почему вы хотели бы использовать willSet,
  но это было ограничено тем, 
  что мы работаем в контексте геометрических форм.
-->

```swift
class TriangleAndSquare {
    var triangle: EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
    }
    var square: Square {
        willSet {
            triangle.sideLength = newValue.sideLength
        }
    }
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}
var triangleAndSquare = TriangleAndSquare(size: 10, name: "еще одна тестовая форма")
print(triangleAndSquare.square.sideLength)
// Выводит "10.0"
print(triangleAndSquare.triangle.sideLength)
// Выводит "10.0"
triangleAndSquare.square = Square(sideLength: 50, name: "больший квадрат")
print(triangleAndSquare.triangle.sideLength)
// Выводит "50.0"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class TriangleAndSquare {
         var triangle: EquilateralTriangle {
             willSet {
                 square.sideLength = newValue.sideLength
             }
         }
         var square: Square {
             willSet {
                 triangle.sideLength = newValue.sideLength
             }
         }
         init(size: Double, name: String) {
             square = Square(sideLength: size, name: name)
             triangle = EquilateralTriangle(sideLength: size, name: name)
         }
     }
  -> var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
  -> print(triangleAndSquare.square.sideLength)
  <- 10.0
  -> print(triangleAndSquare.triangle.sideLength)
  <- 10.0
  -> triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
  -> print(triangleAndSquare.triangle.sideLength)
  <- 50.0
  ```
-->

<!--
  Грамматически, эти клаузы общие для переменных.
  Не уверен, как это может выглядеть
  (и разрешено ли вообще)
  применительно к чему-то за пределами класса или структуры.
-->

При работе с опциональными значениями
вы можете написать `?` перед операциями, такими как методы, свойства и индексирование.
Если значение перед `?` равно `nil`,
все после `?` игнорируется,
и значение всего выражения равно `nil`.
В противном случае опциональное значение распаковывается,
и все после `?` действует на распакованное значение.
В обоих случаях
значение всего выражения является опциональным значением.

```swift
let optionalSquare: Square? = Square(sideLength: 2.5, name: "опциональный квадрат")
let sideLength = optionalSquare?.sideLength
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
  -> let sideLength = optionalSquare?.sideLength
  ```
-->

## Перечисления и Структуры

Используйте `enum` для создания перечисления.
Как и классы и все другие именованные типы,
перечисления могут иметь ассоциированные с ними методы.

<!--
  ОТСЫЛКА
  Игральные карты довольно хорошо подходят для демонстрации перечислений,
  потому что у них есть два аспекта: масть и ранг,
  оба из которых являются частью небольшого конечного набора.
  Используемая здесь колода, вероятно, является наиболее распространенной,
  по крайней мере, в большинстве стран Европы и Америки,
  но существует много других региональных вариаций.
-->

```swift
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king

    func simpleDescription() -> String {
        switch self {
        case .ace:
            return "туз"
        case .jack:
            return "валет"
        case .queen:
            return "дама"
        case .king:
            return "король"
        default:
            return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> enum Rank: Int {
         case ace = 1
         case two, three, four, five, six, seven, eight, nine, ten
         case jack, queen, king
  ---
         func simpleDescription() -> String {
             switch self {
                 case .ace:
                     return "ace"
                 case .jack:
                     return "jack"
                 case .queen:
                     return "queen"
                 case .king:
                     return "king"
                 default:
                     return String(self.rawValue)
             }
         }
     }
  -> let ace = Rank.ace
  -> let aceRawValue = ace.rawValue
  >> print(aceRawValue)
  << 1
  ```
-->

> Эксперимент: Напишите функцию, которая сравнивает два значения типа `Rank`
> путем сравнения их сырых значений.

По умолчанию Swift назначает сырые значения, начиная с нуля
и увеличивая на единицу с каждым шагом,
но вы можете изменить это поведение, явно указав значения.
В приведенном выше примере `Ace` явно задается сырым значением `1`,
и остальные сырые значения присваиваются последовательно.
Также можно использовать строки или числа с плавающей запятой
в качестве сырого типа перечисления.
Используйте свойство `rawValue`, чтобы получить доступ к сырому значению кейса перечисления.

Используйте инициализатор `init?(rawValue:)`
для создания экземпляра перечисления из сырого значения.
Он возвращает либо кейс перечисления, соответствующий сырому значению,
либо `nil`, если нет соответствующего `Rank`.

```swift
if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> if let convertedRank = Rank(rawValue: 3) {
         let threeDescription = convertedRank.simpleDescription()
  >> print(threeDescription)
  << 3
  -> }
  ```
-->

Значения кейсов перечисления - это фактические значения,
а не просто другой способ записи их сырых значений.
Фактически, в случаях, 
когда нет значимого сырого значения,
вам не нужно его предоставлять.

```swift
enum Suit {
    case spades, hearts, diamonds, clubs

    func simpleDescription() -> String {
        switch self {
        case .spades:
            return "пики"
        case .hearts:
            return "червы"
        case .diamonds:
            return "бубны"
        case .clubs:
            return "трефы"
        }
    }
}
let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> enum Suit {
         case spades, hearts, diamonds, clubs
  ---
         func simpleDescription() -> String {
             switch self {
                 case .spades:
                     return "spades"
                 case .hearts:
                     return "hearts"
                 case .diamonds:
                     return "diamonds"
                 case .clubs:
                     return "clubs"
             }
         }
     }
  -> let hearts = Suit.hearts
  -> let heartsDescription = hearts.simpleDescription()
  >> print(heartsDescription)
  << hearts
  ```
-->

> Эксперимент: Добавьте метод `color()` в `Suit`, который возвращает "черный"
> для пик и треф, и возвращает "красный" для червей и бубнов.

<!--
  Масти следуют порядку, используемому в бридже, 
  который соответствует порядку Unicode. В других играх порядок может отличаться. 
  В Википедии перечислено, по меньшей мере, полдюжины порядков.
-->

Обратите внимание на два способа, которыми используется 
кейс перечисления `hearts`: при присвоении значения 
константе `hearts`кейс перечисления `Suit.hearts` 
обозначается своим полным именем, поскольку для 
константы не указан явный тип. Внутри `switch` 
кейс перечисления обозначается 
сокращенной формой `.hearts`, поскольку значение 
`self` уже известно как масть.
Сокращенную форму можно использовать
в любом случае, когда тип значения уже известен.

Если у перечисления есть сырые значения,
они определяются как часть объявления,
что означает, что каждый экземпляр определенного кейса перечисления
всегда имеет одно и то же сырое значение.
Другим выбором для кейсов перечисления
является наличие значений, ассоциированных с кейсом ---
эти значения определяются при создании экземпляра,
и они могут различаться для каждого экземпляра кейса перечисления.
Вы можете рассматривать ассоциированные значения
как хранящиеся свойства экземпляра кейса перечисления.
Например, 
рассмотрим случай запроса
времени восхода и заката с сервера.
Сервер либо отвечает запрошенной информацией,
либо отвечает описанием того, что пошло не так.

<!--
  ОТСЫЛКА
  Серверный ответ - это простой способ в сущности повторно реализовать Optional, 
  обходя тот факт, что я это делаю.

  "Out of cheese" - это ссылка на книгу Терри Пратчетта, 
  в которой фигурирует компьютер по имени Hex. 
  Другие сообщения об ошибках Hex включают:

       - Ошибка "Out of Cheese. Перезапустить с начала".
       - Мистер Джелли! Мистер Джелли! Ошибка по адресу № 6, Трикл-Майн-Роуд.
       - Дыня дыня дыня
       - +++ Вахххх! Моя! +++
       - +++ Ошибка деления на огурец. Пожалуйста, переустановите Вселенную и перезагрузите +++
   - +++ Упс! Идет сыр! +++

  Сами эти сообщения - это отсылки к интерпретаторам BASIC (REDO FROM START) 
  и старым модемам, совместимым с Hayes (+++).

  "Ошибка из-за отсутствия сыра" может быть ссылкой на военный компьютер, 
  хотя я больше не могу найти источник этой истории. 
  По легенде, во время дикой вечеринки один из шкафов вакуумных ламп компьютера 
  был открыт, чтобы обогреть холодную комнату зимой. 
  Чрезвычайное совпадение заключалось в том, что, 
  когда в него врезалась тарелка сыра во время празднества, 
  компьютер продолжал работать, даже если некоторые лампы были сломаны, 
  а на них был разбросан и расплавлен сыр. 
  Техники были отправлены, чтобы убедиться, 
  что с компьютером все в порядке, 
  и им сказали добавить еще сыра, 
  если это необходимо - ответственный офицер сказал, 
  что он не хочет, чтобы "ошибка из-за отсутствия сыра" прервала вычисление
-->

```swift
enum ServerResponse {
    case result(String, String)
    case failure(String)
}

let success = ServerResponse.result("6:00 am", "8:09 pm")
let failure = ServerResponse.failure("Out of cheese.")

switch success {
case let .result(sunrise, sunset):
    print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
case let .failure(message):
    print("Failure...  \(message)")
}
// Выводит "Sunrise is at 6:00 am and sunset is at 8:09 pm."
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> enum ServerResponse {
         case result(String, String)
         case failure(String)
     }
  ---
  -> let success = ServerResponse.result("6:00 am", "8:09 pm")
  -> let failure = ServerResponse.failure("Out of cheese.")
  ---
  -> switch success {
         case let .result(sunrise, sunset):
             print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
         case let .failure(message):
             print("Failure...  \(message)")
     }
  <- Sunrise is at 6:00 am and sunset is at 8:09 pm.
  ```
-->

> Эксперимент: Добавьте третий кейс в `ServerResponse` и в `switch`.

Обратите внимание, как времена восхода и заката
извлекаются из значения `ServerResponse`
в процессе сопоставления значения с кейсами `switch`.

Используйте `struct`, чтобы создать структуру.
Структуры поддерживают многие те же поведения, что и классы,
включая методы и инициализаторы.
Одно из наиболее важных различий
между структурами и классами заключается в том,
что структуры всегда копируются, когда передаются в вашем коде,
в то время как классы передаются по ссылке.

```swift
struct Card {
    var rank: Rank
    var suit: Suit
    func simpleDescription() -> String {
        return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
    }
}
let threeOfSpades = Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription()
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> struct Card {
         var rank: Rank
         var suit: Suit
         func simpleDescription() -> String {
             return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
         }
     }
  -> let threeOfSpades = Card(rank: .three, suit: .spades)
  -> let threeOfSpadesDescription = threeOfSpades.simpleDescription()
  >> print(threeOfSpadesDescription)
  << The 3 of spades
  ```
-->

> Эксперимент: Напишите функцию, которая возвращает массив,
> содержащий полную колоду карт,
> с одной картой для каждой комбинации ранга и масти.

## Конкурентность (Concurrency)

Используйте `async`, чтобы пометить функцию, которая выполняется асинхронно.

```swift
func fetchUserID(from server: String) async -> Int {
    if server == "primary" {
        return 97
    }
    return 501
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func fetchUserID(from server: String) async -> Int {
         if server == "primary" {
             return 97
         }
         return 501
     }
  ```
-->

Вы вызываете асинхронную функцию, добавляя перед ней `await`.

```swift
func fetchUsername(from server: String) async -> String {
    let userID = await fetchUserID(from: server)
    if userID == 501 {
        return "John Appleseed"
    }
    return "Guest"
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func fetchUsername(from server: String) async -> String {
         let userID = await fetchUserID(from: server)
         if userID == 501 {
             return "John Appleseed"
         }
         return "Guest"
     }
  ```
-->

Используйте `async let`, чтобы вызвать асинхронную функцию,
позволяя ей выполняться параллельно с другим асинхронным кодом.
Когда вы используете возвращаемое значение, пишите `await`.

```swift
func connectUser(to server: String) async {
    async let userID = fetchUserID(from: server)
    async let username = fetchUsername(from: server)
    let greeting = await "Hello \(username), user ID \(userID)"
    print(greeting)
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func connectUser(to server: String) async {
         async let userID = fetchUserID(from: server)
         async let username = fetchUsername(from: server)
         let greeting = await "Hello \(username), user ID \(userID)"
         print(greeting)
     }
  ```
-->

Используйте `Task`, чтобы вызывать асинхронные функции из синхронного кода,
не дожидаясь их завершения.

```swift
Task {
    await connectUser(to: "primary")
}
// Выводит "Hello Guest, user ID 97"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> Task {
         await connectUser(to: "primary")
     }
  >> import Darwin; sleep(1)  // Pause for task to run
  <- Hello Guest, user ID 97
  ```
-->

Используйте группы задач для организации конкурентного кода.

```swift
let userIDs = await withTaskGroup(of: Int.self) { group in
    for server in ["primary", "secondary", "development"] {
        group.addTask {
            return await fetchUserID(from: server)
        }
    }

    var results: [Int] = []
    for await result in group {
        results.append(result)
    }
    return results
}
```

Акторы похожи на классы,
за исключением того, что они гарантируют безопасное взаимодействие
различных асинхронных функций с экземпляром одного и того же актора одновременно.

```swift
actor ServerConnection {
    var server: String = "primary"
    private var activeUsers: [Int] = []
    func connect() async -> Int {
        let userID = await fetchUserID(from: server)
        // ... общение с сервером ...
        activeUsers.append(userID)
        return userID
    }
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> actor Oven {
         var contents: [String] = []
         func bake(_ food: String) -> String {
             contents.append(food)
             // ... wait for food to bake ...
             return contents.removeLast()
         }
     }
  ```
-->

При вызове метода на акторе или доступе к его свойствам
вы помечаете этот код `await`,
чтобы указать, что он может потребовать ожидания другого кода,
который уже выполняется на акторе, для завершения.

```swift
let server = ServerConnection()
let userID = await server.connect()
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let oven = Oven()
  -> let biscuits = await oven.bake("biscuits")
  ```
-->


## Протоколы и Расширения

Используйте `protocol` для объявления протокола.

```swift
protocol ExampleProtocol {
     var simpleDescription: String { get }
     mutating func adjust()
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> protocol ExampleProtocol {
          var simpleDescription: String { get }
          mutating func adjust()
     }
  ```
-->

Классы, перечисления и структуры могут все принимать протоколы.

<!--
  ОТСЫЛКА
  Использование adjust() полностью является 
  заполнителем для более интересной операции. 
  Точно так же и для структур и классов - 
  это заполнители для более интересных структур данных.
-->

```swift
class SimpleClass: ExampleProtocol {
     var simpleDescription: String = "A very simple class."
     var anotherProperty: Int = 69105
     func adjust() {
          simpleDescription += "  Now 100% adjusted."
     }
}
var a = SimpleClass()
a.adjust()
let aDescription = a.simpleDescription

struct SimpleStructure: ExampleProtocol {
     var simpleDescription: String = "A simple structure"
     mutating func adjust() {
          simpleDescription += " (adjusted)"
     }
}
var b = SimpleStructure()
b.adjust()
let bDescription = b.simpleDescription
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> class SimpleClass: ExampleProtocol {
          var simpleDescription: String = "A very simple class."
          var anotherProperty: Int = 69105
          func adjust() {
               simpleDescription += "  Now 100% adjusted."
          }
     }
  -> var a = SimpleClass()
  -> a.adjust()
  -> let aDescription = a.simpleDescription
  >> print(aDescription)
  << A very simple class.  Now 100% adjusted.
  ---
  -> struct SimpleStructure: ExampleProtocol {
          var simpleDescription: String = "A simple structure"
          mutating func adjust() {
               simpleDescription += " (adjusted)"
          }
     }
  -> var b = SimpleStructure()
  -> b.adjust()
  -> let bDescription = b.simpleDescription
  >> print(bDescription)
  << A simple structure (adjusted)
  ```
-->

> Эксперимент: Добавьте еще одно требование к `ExampleProtocol`. 
> Какие изменения вам нужно внести 
> в `SimpleClass` и `SimpleStructure`, 
> чтобы они по-прежнему соответствовали протоколу?

Обратите внимание на использование ключевого слова `mutating` 
при объявлении `SimpleStructure` 
для обозначения метода, изменяющего структуру. 
Объявление `SimpleClass` не требует маркировки 
методов как `mutating`, потому что методы 
класса всегда могут изменять класс.

Используйте `extension`, чтобы добавить функциональность к существующему типу, 
такую как новые методы и вычисляемые свойства. 
Вы можете использовать расширение для добавления соответствия протоколу к типу, 
объявленному в другом месте, или даже к типу, 
который вы импортировали из библиотеки или фреймворка.

```swift
extension Int: ExampleProtocol {
    var simpleDescription: String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
 }
print(7.simpleDescription)
// Выводит "The number 7"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> extension Int: ExampleProtocol {
         var simpleDescription: String {
             return "The number \(self)"
         }
         mutating func adjust() {
             self += 42
         }
      }
  -> print(7.simpleDescription)
  <- The number 7
  ```
-->

> Эксперимент: Напишите расширение для типа `Double`,
> которое добавляет свойство `absoluteValue`.

Вы можете использовать имя протокола так же, 
как и любой другой именованный тип, 
например, чтобы создать коллекцию объектов разных типов, 
которые все соответствуют одному протоколу. 
Когда вы работаете с значениями, тип которых является упакованным 
протокольным типом, методы за пределами определения протокола не доступны.

```swift
let protocolValue: any ExampleProtocol = a
print(protocolValue.simpleDescription)
// Выводит "A very simple class.  Now 100% adjusted."
// print(protocolValue.anotherProperty)  // Раскомментируйте, чтобы увидеть ошибку
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let protocolValue: ExampleProtocol = a
  -> print(protocolValue.simpleDescription)
  <- A very simple class.  Now 100% adjusted.
  // print(protocolValue.anotherProperty)  // Uncomment to see the error
  ```
-->

Несмотря на то что переменная `protocolValue` 
имеет тип времени выполнения `SimpleClass`, 
компилятор рассматривает ее как заданный тип `ExampleProtocol`. 
Это означает, что вы не можете случайно 
обращаться к методам или свойствам, 
которые класс реализует, помимо своего соответствия протоколу.

## Обработка ошибок

Ошибки представляются с использованием любого типа, который принимает протокол `Error`.

<!--
  ОТСЫЛКА
  `PrinterError.OnFire` — это ссылка на сообщение об ошибке "lp0 on fire" в 
  системе печати Unix, используемое, когда ядро не может определить конкретную 
  ошибку. Имена принтеров, использованные в примерах в этом разделе, 
  являются именами людей, которые имели важное значение в развитии печати.
  
  Би Шэн считается изобретателем первого подвижного типа, изготовленного из фарфора, 
  в Китае в 1040-х годах. Это было в значительной степени неудачным изобретением, 
  главным образом из-за огромного количества символов, необходимых для написания 
  китайского языка, и не удалось заменить древесную типографию. Иоганн Гутенберг 
  заслуживает признание как первый европеец, использовавший подвижный тип в 1440-х
  годах. Его металлический тип возможствовал печатной революции. Отмар Мергенталер
  изобрел машину Лайнотип в 1884 году, что существенно увеличило скорость верстки 
  типографского текста по сравнению с предыдущей ручнойверсткой. Она устанавливала
  целую строку типа (отсюда и название) за один раз и управлялась клавиатурой. 
  Машина Monotype, изобретенная в 1885 году Толбертом Лэнстоном, выполняла подобную работу.
-->

```swift
enum PrinterError: Error {
    case outOfPaper
    case noToner
    case onFire
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> enum PrinterError: Error {
         case outOfPaper
         case noToner
         case onFire
     }
  ```
-->

Используйте `throw` для генерации ошибки 
и `throws` для обозначения функции, которая может генерировать ошибку. 
Если вы вызываете ошибку внутри функции, 
функция немедленно возвращает управление, и код, вызвавший функцию, 
обрабатывает ошибку.

```swift
func send(job: Int, toPrinter printerName: String) throws -> String {
    if printerName == "Never Has Toner" {
        throw PrinterError.noToner
    }
    return "Job sent"
}
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func send(job: Int, toPrinter printerName: String) throws -> String {
         if printerName == "Never Has Toner" {
             throw PrinterError.noToner
         }
         return "Job sent"
     }
  ```
-->

Существует несколько способов обработки ошибок. 
Один из способов - использование конструкции `do`-`catch`. 
Внутри блока `do` вы отмечаете код, 
который может вызвать ошибку, 
написав перед ним `try`. 
В блоке `catch` ошибка автоматически 
получает имя `error`, если вы не присвоили ей другое имя.

```swift
do {
    let printerResponse = try send(job: 1040, toPrinter: "Bi Sheng")
    print(printerResponse)
} catch {
    print(error)
}
// Выводит "Job sent"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> do {
         let printerResponse = try send(job: 1040, toPrinter: "Bi Sheng")
         print(printerResponse)
     } catch {
         print(error)
     }
  <- Job sent
  ```
-->

> Эксперимент: Измените имя принтера на `"Never Has Toner"`,
> чтобы функция `send(job:toPrinter:)` вызвала ошибку.

<!--
    Утверждение проверяет изменение, указанное в блоке "Эксперимент".
-->

<!--
  - test: `guided-tour`

  ```swifttest
  >> do {
         let printerResponse = try send(job: 500, toPrinter: "Never Has Toner")
         print(printerResponse)
     } catch {
         print(error)
     }
  <- noToner
  ```
-->

Вы можете предоставить несколько блоков `catch`, 
которые обрабатывают конкретные ошибки. 
Вы указываете шаблон после `catch`, 
так же, как и после `case` в операторе `switch`.

<!--
    ОТСЫЛКА 
    Фраза "остальная часть в огне" взята из сериала "IT Crowd", сезон 1, эпизод 2.
-->

```swift
do {
    let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
    print(printerResponse)
} catch PrinterError.onFire {
    print("I'll just put this over here, with the rest of the fire.")
} catch let printerError as PrinterError {
    print("Printer error: \(printerError).")
} catch {
    print(error)
}
// Выводит "Job sent"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> do {
         let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
         print(printerResponse)
     } catch PrinterError.onFire {
         print("I'll just put this over here, with the rest of the fire.")
     } catch let printerError as PrinterError {
         print("Printer error: \(printerError).")
     } catch {
         print(error)
     }
  <- Job sent
  ```
-->

> Эксперимент: Добавьте код для генерации ошибки внутри блока `do`.
> Какую ошибку нужно сгенерировать,
> чтобы она обрабатывалась первым блоком `catch`?
> А что насчет второго и третьего блоков?

Другой способ обработки ошибок - 
использовать `try?` для преобразования результата в optional. 
Если функция генерирует ошибку, конкретная ошибка отбрасывается, 
и результат равен `nil`. 
В противном случае результат - это optional, 
содержащий значение, возвращенное функцией.

```swift
let printerSuccess = try? send(job: 1884, toPrinter: "Mergenthaler")
let printerFailure = try? send(job: 1885, toPrinter: "Never Has Toner")
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> let printerSuccess = try? send(job: 1884, toPrinter: "Mergenthaler")
  >> print(printerSuccess as Any)
  << Optional("Job sent")
  -> let printerFailure = try? send(job: 1885, toPrinter: "Never Has Toner")
  >> print(printerFailure as Any)
  << nil
  ```
-->

Используйте `defer`, чтобы написать блок кода,
который выполняется после всех остальных участков кода в функции,
непосредственно перед возвратом из функции.
Этот код выполняется независимо от того, вызывает ли функция ошибку или нет.
`defer` позволяет вам разместить код настройки и очистки рядом друг с другом,
даже если они должны выполняться в разные моменты времени.

```swift
var fridgeIsOpen = false
let fridgeContent = ["milk", "eggs", "leftovers"]

func fridgeContains(_ food: String) -> Bool {
    fridgeIsOpen = true
    defer {
        fridgeIsOpen = false
    }

    let result = fridgeContent.contains(food)
    return result
}
if fridgeContains("banana") {
    print("Found a banana")
}
print(fridgeIsOpen)
// Выводит "false"
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> var fridgeIsOpen = false
  -> let fridgeContent = ["milk", "eggs", "leftovers"]
  ---
  -> func fridgeContains(_ food: String) -> Bool {
         fridgeIsOpen = true
         defer {
             fridgeIsOpen = false
         }
  ---
         let result = fridgeContent.contains(food)
         return result
     }
  >> let containsBanana =
  -> fridgeContains("banana")
  >> print(containsBanana)
  << false
  -> print(fridgeIsOpen)
  <- false
  ```
-->

## Общие сведения 

Укажите имя в угловых скобках,
чтобы создать обобщенную функцию или тип.

<!--
  ОТСЫЛКА
  Четыре стука - это отсылка к четвёртому сезону
  сериала "Доктор Кто", в котором четыре 
  стука играют важную роль в сюжете сезона.
-->

```swift
func makeArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
    var result: [Item] = []
    for _ in 0..<numberOfTimes {
         result.append(item)
    }
    return result
}
makeArray(repeating: "knock", numberOfTimes: 4)
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func makeArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
         var result: [Item] = []
         for _ in 0..<numberOfTimes {
              result.append(item)
         }
         return result
     }
  >> let fourKnocks =
  -> makeArray(repeating: "knock", numberOfTimes: 4)
  >> print(fourKnocks)
  << ["knock", "knock", "knock", "knock"]
  ```
-->

Вы можете создавать обобщенные формы функций и методов,
а также классов, перечислений и структур.

```swift
// Reimplement the Swift standard library's optional type
enum OptionalValue<Wrapped> {
    case none
    case some(Wrapped)
}
var possibleInteger: OptionalValue<Int> = .none
possibleInteger = .some(100)
```

<!--
  - test: `guided-tour`

  ```swifttest
  // Reimplement the Swift standard library's optional type
  -> enum OptionalValue<Wrapped> {
         case none
         case some(Wrapped)
     }
  -> var possibleInteger: OptionalValue<Int> = .none
  -> possibleInteger = .some(100)
  ```
-->

Используйте 'where' непосредственно перед телом
для указания списка требований —
например,
чтобы потребовать, чтобы тип реализовывал протокол,
чтобы два типа были одинаковыми
или чтобы класс имел конкретный суперкласс.

```swift
func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
    where T.Element: Equatable, T.Element == U.Element
{
    for lhsItem in lhs {
        for rhsItem in rhs {
            if lhsItem == rhsItem {
                return true
            }
        }
    }
   return false
}
anyCommonElements([1, 2, 3], [3])
```

<!--
  - test: `guided-tour`

  ```swifttest
  -> func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
         where T.Element: Equatable, T.Element == U.Element
     {
         for lhsItem in lhs {
             for rhsItem in rhs {
                 if lhsItem == rhsItem {
                     return true
                 }
             }
         }
        return false
     }
  >> let hasAnyCommon =
  -> anyCommonElements([1, 2, 3], [3])
  >> print(hasAnyCommon)
  << true
  ```
-->

> Эксперимент: Измените функцию `anyCommonElements(_:_:)`,
> чтобы создать функцию, возвращающую массив
> общих элементов двух последовательностей.

Запись `<T: Equatable>` 
эквивалентна записи `<T> ... where T: Equatable`.

<!--
Этот исходный файл является частью проекта с открытым исходным кодом Swift.org.

Авторские права (c) 2014 - 2022 гг. Apple Inc. и авторы проекта Swift
Лицензировано по Apache License v2.0 с исключением из библиотеки выполнения

См. https://swift.org/LICENSE.txt для информации о лицензии
См. https://swift.org/CONTRIBUTORS.txt для списка авторов проекта Swift
-->
