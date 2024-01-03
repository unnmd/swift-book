# Основы

Работайте с общими видами данных и пишите базовый синтаксис.

Swift предоставляет множество фундаментальных типов данных,
включая `Int` для целых чисел,
`Double` для чисел с плавающей запятой,
`Bool` для булевых значений,
и `String` для текста.
Swift также предоставляет мощные версии трех основных типов коллекций,
`Array`, `Set` и `Dictionary`,
как описано в <doc:CollectionTypes>.

Swift использует переменные для хранения и ссылки на значения по идентификационному 
имени. Swift также широко использует переменные, значения которых не могут быть 
изменены. Эти переменные известны как константы и используются во всем Swift для
обеспечения безопасности кода и ясности намерений при работе с значениями, которые не должны изменяться.

Помимо знакомых типов, Swift представляет продвинутые типы, такие как кортежи. 
Кортежи позволяют вам создавать и передавать группировки значений. Вы можете 
использовать кортеж для возврата нескольких значений из функции как единого 
составного значения.

Swift также вводит опциональные типы, 
которые обрабатывают отсутствие значения. 
Опционалы говорят либо "здесь *есть* значение, 
и оно равно *x*", либо "здесь *нет* значения вообще".

Swift является *типобезопасным* языком, что означает, что язык помогает вам быть
ясным относительно типов значений, с которыми ваш код может работать. 
Если часть вашего кода требует `String`, типовая безопасность предотвращает 
передачу ей по ошибке `Int`. Точно так же типовая безопасность мешает вам 
случайно передавать опциональную `String` в участок кода, который требует 
неопциональную `String`. 
Типовая безопасность помогает вам выявлять и устранять 
ошибки как можно раньше впроцессе разработки.

## Константы и Переменные

Константы и переменные связывают имя
(например, `maximumNumberOfLoginAttempts` или `welcomeMessage`)
со значением определенного типа
(например, число `10` или строка `"Hello"`).
Значение *константы* не может быть изменено после установки,
в то время как *переменная* может быть установлена на другое значение в будущем.

### Объявление Констант и Переменных

Константы и переменные должны быть объявлены перед их использованием.
Константы объявляются с использованием ключевого слова `let`,
а переменные — с использованием ключевого слова `var`.
Вот пример того, как константы и переменные могут быть использованы
для отслеживания количества попыток входа пользователя:

```swift
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
```

<!--
  - test: `constantsAndVariables`

  ```swifttest
  -> let maximumNumberOfLoginAttempts = 10
  -> var currentLoginAttempt = 0
  ```
-->

Этот код можно прочитать следующим образом:

"Объявить новую константу с именем `maximumNumberOfLoginAttempts`
и присвоить ей значение `10`.
Затем объявить новую переменную с именем `currentLoginAttempt`
и присвоить ей начальное значение `0`."

В этом примере
максимальное количество разрешенных попыток входа объявлено как константа,
поскольку максимальное значение никогда не изменяется.
Счетчик текущей попытки входа объявлен как переменная,
потому что это значение должно увеличиваться после каждой неудачной попытки входа.

Если сохраненное значение в вашем коде не будет изменяться,
всегда объявляйте его как константу с использованием ключевого слова `let`.
Используйте переменные только для хранения значений, которые изменяются.

При объявлении константы или переменной
вы можете присвоить ей значение как часть этого объявления,
как показано в приведенных выше примерах.
В качестве альтернативы
вы можете присвоить ей начальное значение позже в программе,
при условии, что гарантируется, что у нее будет значение
перед первым чтением из нее.

```swift
var environment = "development"
let maximumNumberOfLoginAttempts: Int
// Переменной maximumNumberOfLoginAttempts ещё не присвоено значение.

if environment == "development" {
    maximumNumberOfLoginAttempts = 100
} else {
    maximumNumberOfLoginAttempts = 10
}
// Теперь у переменной maximumNumberOfLoginAttempts есть значение и его можно прочитать.
```

<!--
  - test: `constantsWithDeferredInitialization`

  ```swifttest
  -> var environment = "development"
  -> let maximumNumberOfLoginAttempts: Int
  -> if environment == "development" {
         maximumNumberOfLoginAttempts = 100
     } else {
         maximumNumberOfLoginAttempts = 10
     }
  >> print(maxNumberOfLoginAttempts)
  << 100
  ```
-->

В этом примере максимальное количество 
попыток входа является константой, 
и его значение зависит от окружения. 
В среде разработки у него значение 100; 
в любой другой среде его значение равно 10. 
Обе ветви оператора `if` инициализируют `maximumNumberOfLoginAttempts` 
какое-то значение, гарантируя, 
что константе всегда присваивается значение. 
Для получения информации о том, 
как Swift проверяет ваш код 
при установке начального значения, таким образом, 
см. <doc:Declarations#Constant-Declaration>.

Вы можете объявить несколько констант или переменных в одной строке, 
разделяя их запятыми:

```swift
var x = 0.0, y = 0.0, z = 0.0
```

<!--
  - test: `multipleDeclarations`

  ```swifttest
  -> var x = 0.0, y = 0.0, z = 0.0
  >> print(x, y, z)
  << 0.0 0.0 0.0
  ```
-->

### Аннотации Типов

Вы можете предоставить *аннотацию типа* при объявлении константы или переменной,
чтобы явно указать тип значений, которые может хранить константа или переменная.
Напишите аннотацию типа, разместив двоеточие после имени константы или 
переменной, за которым следует пробел, а затем имя типа для использования.

В этом примере предоставлена аннотация типа для переменной с именем `welcomeMessage`,
чтобы указать, что переменная может хранить значения типа `String`:

```swift
var welcomeMessage: String
```

<!--
  - test: `typeAnnotations`

  ```swifttest
  -> var welcomeMessage: String
  ```
-->

Двоеточие в объявлении означает "...типа...", 
поэтому код выше можно прочитать как:

"Объявить переменную с именем `welcomeMessage` типа `String`."

Фраза "типа `String`" означает "может хранить любое значение типа `String`". 
Представьте себе это как описание "типа вещи" (или "вида вещи"), которую можно хранить.

Переменной `welcomeMessage` теперь можно присвоить любое строковое значение без ошибок:

```swift
welcomeMessage = "Hello"
```

<!--
  - test: `typeAnnotations`

  ```swifttest
  -> welcomeMessage = "Hello"
  >> print(welcomeMessage)
  << Hello
  ```
-->

Вы можете определить несколько связанных переменных одного типа в одной строке, 
разделяя их запятыми, с одной аннотацией типа после последнего имени переменной:

```swift
var red, green, blue: Double
```

<!--
  - test: `typeAnnotations`

  ```swifttest
  -> var red, green, blue: Double
  ```
-->

> Примечание: В практике редко требуется написание аннотаций типов. 
> Если вы предоставляете начальное значение для константы или переменной в том 
> месте, где она определена, Swift почти всегда может самостоятельно вывести 
> тип для использования этой константы или переменной, как описано в
> <doc:TheBasics#Type-Safety-and-Type-Inference>. В приведенном выше примере 
> `welcomeMessage` не предоставляется начальное значение, поэтому тип переменной
> `welcomeMessage` указывается аннотацией типа, а не выводится из начального значения.

### Именование Констант и Переменных

Имена констант и переменных могут содержать практически любой символ, 
включая символы Unicode:

```swift
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

<!--
  - test: `constantsAndVariables`

  ```swifttest
  -> let π = 3.14159
  -> let 你好 = "你好世界"
  -> let 🐶🐮 = "dogcow"
  ```
-->

Имена констант и переменных не могут содержать пробельные символы, 
математические символы, стрелки, значения юникодных скаляров для личного 
использования, а также символы линий и рамок. 
Они также не могут начинаться с цифры, 
хотя числа могут включаться в других частях имени.

После того как вы объявили константу или переменную определенного типа, 
вы не можете объявить ее снова с тем же именем или изменить ее, 
чтобы хранить значения другого типа. 
Вы также не можете изменить константу на переменную 
или наоборот.

> Примечание: Если вам нужно дать константе или переменной то же имя, что и зарезервированное ключевое слово
> Swift, окружите ключевое слово обратными кавычками (`` ` ``) при использовании его в качестве имени. 
> Однако избегайте использования ключевых слов в качестве имен, если у вас есть альтернативы.

Значение существующей переменной можно изменить на другое значение совместимого типа. 
В этом примере значение `friendlyWelcome` изменяется с 
`"Hello!"` на `"Bonjour!"`:

```swift
var friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// friendlyWelcome теперь "Bonjour!"
```

<!--
  - test: `constantsAndVariables`

  ```swifttest
  -> var friendlyWelcome = "Hello!"
  -> friendlyWelcome = "Bonjour!"
  /> friendlyWelcome is now \"\(friendlyWelcome)\"
  </ friendlyWelcome is now "Bonjour!"
  ```
-->

В отличие от переменной, значение константы не может быть изменено после установки. 
Попытка сделать это вызовет ошибку во время компиляции:

```swift
let languageName = "Swift"
languageName = "Swift++"
// Это ошибка времени компиляции: languageName нельзя изменить.
```

<!--
  - test: `constantsAndVariables_err`

  ```swifttest
  -> let languageName = "Swift"
  -> languageName = "Swift++"
  // This is a compile-time error: languageName cannot be changed.
  !$ error: cannot assign to value: 'languageName' is a 'let' constant
  !! languageName = "Swift++"
  !! ^~~~~~~~~~~~
  !! /tmp/swifttest.swift:1:1: note: change 'let' to 'var' to make it mutable
  !! let languageName = "Swift"
  !! ^~~
  !! var
  ```
-->

### Печать Констант и Переменных

Вы можете напечатать текущее значение константы или переменной с помощью функции `print(_:separator:terminator:)`:

```swift
print(friendlyWelcome)
// Печатает "Bonjour!"
```

<!--
  - test: `constantsAndVariables`

  ```swifttest
  -> print(friendlyWelcome)
  <- Bonjour!
  ```
-->

Функция `print(_:separator:terminator:)` является глобальной функцией, 
которая выводит одно или несколько значений в соответствующий вывод. 
Например, в Xcode функция 
`print(_:separator:terminator:)` выводит результат в 
"консольное" окно Xcode. Параметры `separator` и `terminator` имеют значения по 
умолчанию, поэтому вы можете опустить их при вызове этой функции.
По умолчанию функция завершает строку, 
добавляя перевод строки после печатаемого значения. 
Чтобы вывести значение без перевода строки после него, 
передайте пустуюстроку в качестве аргумента `terminator` — 
например, `print(someValue, terminator: "")`. 
Дополнительную информацию о параметрах со значениями по умолчанию можно найти в 
разделе <doc:Functions#Default-Parameter-Values>.

<!--
  - test: `printingWithoutNewline`

  ```swifttest
  >> let someValue = 10
  -> print(someValue, terminator: "")
  -> print(someValue)
  << 1010
  ```
-->

<!--
  ВОПРОС: я правильно обратился к консоли Xcode здесь? 
  Следует ли упомянуть другие потоки вывода, такие как REPL / песочницы?
-->

<!--
  ПРИМЕЧАНИЕ: это преднамеренно упрощенное описание того, что вы можете сделать с функцией print(). 
  Позже оно будет расширено.
-->

Swift использует *интерполяцию строк* для включения имени константы или переменной
в качестве заполнителя в более длинной строке и для того, чтобы побудить Swift 
заменить его текущим значением этой константы или переменной. Оберните имя в 
круглые скобки и предварительно экранируйте его обратным слешем перед открывающей круглой скобкой:

```swift
print("The current value of friendlyWelcome is \(friendlyWelcome)")
// Prints "The current value of friendlyWelcome is Bonjour!"
```

<!--
  - test: `constantsAndVariables`

  ```swifttest
  -> print("The current value of friendlyWelcome is \(friendlyWelcome)")
  <- The current value of friendlyWelcome is Bonjour!
  ```
-->

> Примечание: Все варианты использования интерполяции строк описаны 
> в разделе <doc:StringsAndCharacters#String-Interpolation>.

## Комментарии

Используйте комментарии для включения неисполняемого текста в ваш код в виде 
заметки или напоминания для себя. 
Комментарии игнорируются компилятором Swift при компиляции вашего кода.

Комментарии в Swift очень похожи на комментарии в C. 
Однострочные комментарии начинаются с двух косых черт (`//`):

```swift
// Это комментарий.
```

<!--
  - test: `comments`

  ```swifttest
  -> // This is a comment.
  ```
-->

Многострочные комментарии начинаются с косой черты, за которой следует звезда (`/*`),
и заканчиваются звездой, за которой следует косая черта (`*/`):

```swift
/* Это также комментарий,
но написанный на нескольких строках. */
```

<!--
  - test: `comments`

  ```swifttest
  -> /* This is also a comment
     but is written over multiple lines. */
  ```
-->

В отличие от многострочных комментариев в C, многострочные комментарии в Swift 
могут быть вложены друг в друга. Вы создаете вложенные комментарии, 
начиная блок многострочного комментария, а затем начиная второй многострочный 
комментарий внутри первого блока. Затем второй блок закрывается, 
за которым следует первый блок:

```swift
/* Это начало первого многострочного комментария.
    /* Это второй, вложенный многострочный комментарий. */
Это конец первого многострочного комментария. */
```

<!--
  - test: `comments`

  ```swifttest
  -> /* This is the start of the first multiline comment.
        /* This is the second, nested multiline comment. */
     This is the end of the first multiline comment. */
  ```
-->

Вложенные многострочные комментарии позволяют вам быстро и легко комментировать 
большие блоки кода, даже если код уже содержит многострочные комментарии.

## Точки с запятой

В отличие от многих других языков программирования, в Swift нет обязательства 
ставить точку с запятой (`;`) после каждого оператора в вашем коде, 
хотя вы можете сделать это, если хотите. 
Однако точки с запятой *обязательны*, 
если вы хотите написать несколько отдельных операторов в одной строке:

```swift
let cat = "🐱"; print(cat)
// Выводит "🐱"
```

<!--
  - test: `semiColons`

  ```swifttest
  -> let cat = "🐱"; print(cat)
  <- 🐱
  ```
-->

## Целые числа

*Целые числа* - это целые числа без дробной части, 
такие как `42` и `-23`. 
Целые числа бывают *знаковыми* (положительные, ноль или отрицательные)
или *беззнаковыми* (положительные или ноль).

Swift предоставляет знаковые и беззнаковые целые числа в формах 8, 16, 32 и 64 бита. 
Эти целые числа следуют конвенции имен, аналогичной C, 
где 8-битное беззнаковое целое число имеет тип `UInt8`, 
а 32-битное знаковое целое число - тип `Int32`. Как и все типы в Swift, 
эти типы целых чисел начинаются с заглавной буквы.

### Границы целых чисел

Вы можете получить доступ к минимальным и максимальным значениям каждого типа 
целого числа с использованием свойств `min` и `max`:

```swift
let minValue = UInt8.min  // minValue равно 0, и имеет тип UInt8
let maxValue = UInt8.max  // maxValue равно 255, и имеет тип UInt8
```

<!--
  - test: `integerBounds`

  ```swifttest
  -> let minValue = UInt8.min  // minValue равно 0, и имеет тип UInt8
  -> let maxValue = UInt8.max  // maxValue равно 255, и имеет тип UInt8
  >> print(minValue, maxValue)
  << 0 255
  ```
-->

Значения этих свойств соответствуют числам с соответствующим размером (например,
`UInt8` в приведенном выше примере) и, следовательно, 
могут использоваться в выражениях вместе с другими значениями того же типа.

### Int

В большинстве случаев вам не нужно выбирать конкретный размер целого числа для 
использования в вашем коде.  Swift предоставляет дополнительный тип целого числа, Int, 
который имеет тот же размер, что и разрядность вашей системы:

- На 32-битной платформе `Int` имеет тот же размер, что и `Int32`.
- На 64-битной платформе `Int` имеет тот же размер, что и `Int64`.

Если вам не нужно работать с конкретным размером целого числа, всегда 
используйте `Int` для целочисленных значений в вашем коде. 
Это способствует согласованности кода и взаимодействию. 
Даже на 32-битных платформах `Int` может хранить любое значение между 
`-2,147,483,648` и `2,147,483,647` и достаточно велико для многих диапазонов целых чисел.

### UInt

Swift также предоставляет беззнаковый тип целого числа, `UInt`, 
который имеет тот же размер, что и разрядность вашей системы:

- На 32-битной платформе `UInt` имеет тот же размер, что и `UInt32`.
- На 64-битной платформе `UInt` имеет тот же размер, что и `UInt64`.

> Примечание: Используйте `UInt` только тогда, когда вам действительно нужен 
> беззнаковый тип целого числа с тем же размером, что и разрядность вашей системы.
> Если это не так, предпочтительнее использовать `Int`, даже когда известно, что
> значения будут неотрицательными. Согласованное использование `Int` для 
> целочисленных значений облегчит взаимодействие с кодом, избежит необходимости 
> конвертировать между различными типами чисел и соответствует выводу типа для 
> целых чисел, как описано в <doc:TheBasics#Type-Safety-and-Type-Inference>.

## Дробные числа с плавающей запятой

*Дробные числа с плавающей запятой* представляют собой числа с дробной частью,
такие как `3.14159`, `0.1` и `-273.15`.

Типы дробных чисел могут представлять гораздо более широкий диапазон значений, чем целочисленные типы,
и могут хранить числа, которые намного больше или меньше тех, что могут быть сохранены в `Int`.
Swift предоставляет два знаковых типа дробных чисел:

- `Double` представляет собой 64-битное дробное число.
- `Float` представляет собой 32-битное дробное число.

> Примечание: `Double` имеет точность не менее 15 десятичных знаков,
> в то время как точность `Float` может быть всего 6 десятичных знаков.
> Выбор между типами дробных чисел зависит от характера и диапазона
> значений, с которыми вам нужно работать в вашем коде.
> В ситуациях, где подходит любой из типов, предпочтительнее использовать `Double`.

<!--
  TODO: Явно упомянуть ситуации, когда Float подходит,
  например, при оптимизации размера для коллекций?
-->

<!--
  TODO: упомянуть бесконечность, -бесконечность и т.д.
-->

## Безопасность типов и вывод типов

Swift - *язык со строгой типизацией*.
Язык со строгой типизацией побуждает вас быть ясными относительно
типов значений, с которыми ваш код может работать.
Если часть вашего кода требует `String`, вы не сможете передать в нее `Int` по ошибке.

Поскольку Swift является языком со строгой типизацией,
он выполняет *проверку типов* при компиляции вашего кода
и выдает сообщения об ошибках при несоответствии типов.
Это позволяет вам выявлять и устранять ошибки на ранних этапах разработки.

Проверка типов помогает вам избегать ошибок при работе с различными типами значений.
Однако это не означает, что вы должны указывать тип
каждой константе и переменной, которую вы объявляете.
Если вы не указываете тип значения,
Swift использует *вывод типов*, чтобы определить соответствующий тип.
Вывод типов позволяет компилятору
автоматически выводить тип конкретного выражения при компиляции вашего кода,
просто анализируя предоставленные значения.

Из-за вывода типов Swift требует гораздо меньше объявлений типов,
чем языки, такие как C или Objective-C.
Константы и переменные по-прежнему имеют явные типы,
но большая часть работы по указанию их типов делается за вас.

Вывод типов особенно полезен
при объявлении констант или переменных с начальным значением.
Это часто делается с использованием *литерального значения* (или *литерала*),
присваиваемого константе или переменной в момент ее объявления.
(Литеральное значение - это значение, которое прямо встроено в ваш исходный код,
как `42` и `3.14159` в приведенных ниже примерах.)

Например, если вы присваиваете литеральное значение `42` новой константе,
не указывая при этом тип, Swift вычисляет, что вы хотите,
чтобы константа была типа `Int`,
поскольку вы инициализировали ее числом, похожим на целое:

```swift
let meaningOfLife = 42
// meaningOfLife выводится как тип Int
```

<!--
  - test: `typeInference`

  ```swifttest
  -> let meaningOfLife = 42
  // meaningOfLife is inferred to be of type Int
  >> print(type(of: meaningOfLife))
  << Int
  ```
-->

Точно так же, если вы не указываете тип для литерала с плавающей точкой,
Swift выводит, что вы хотите создать `Double`:

```swift
let pi = 3.14159
// pi выводится как тип Double
```

<!--
  - test: `typeInference`

  ```swifttest
  -> let pi = 3.14159
  // pi is inferred to be of type Double
  >> print(type(of: pi))
  << Double
  ```
-->

Swift всегда выбирает `Double` (а не `Float`)
при выводе типа чисел с плавающей запятой.

Если вы комбинируете литералы целых и дробных чисел в выражении,
тип `Double` будет выведен из контекста:

```swift
let anotherPi = 3 + 0.14159
// anotherPi также выводится как тип Double
```
<!--
  - test: `typeInference`

  ```swifttest
  -> let anotherPi = 3 + 0.14159
  // anotherPi is also inferred to be of type Double
  >> print(type(of: anotherPi))
  << Double
  ```
-->


Литеральное значение `3` не имеет явного типа само по себе,
и поэтому подходящий выходной тип `Double` выводится
из-за присутствия литерала с плавающей точкой в составе сложения.

## Числовые литералы

Целочисленные литералы можно записывать следующим образом:

- *Десятичное* число, без префикса
- *Двоичное* число, с префиксом `0b`
- *Восьмеричное* число, с префиксом `0o`
- *Шестнадцатеричное* число, с префиксом `0x`

Все эти целочисленные литералы имеют десятичное значение `17`:

```swift
let decimalInteger = 17
let binaryInteger = 0b10001       // 17 в двоичной записи
let octalInteger = 0o21       // 17 в восьмеричной записи
let hexadecimalInteger = 0x11 // 17 в шестнадцатеричной записи
```

<!--
  - test: `numberLiterals`

  ```swifttest
  -> let decimalInteger = 17
  -> let binaryInteger = 0b10001       // 17 in binary notation
  -> let octalInteger = 0o21           // 17 in octal notation
  -> let hexadecimalInteger = 0x11     // 17 in hexadecimal notation
  >> print(binaryInteger, octalInteger, hexadecimalInteger)
  << 17 17 17
  ```
-->

Литералы с плавающей запятой могут быть десятичными (без префикса)
или шестнадцатеричными (с префиксом `0x`).
Они всегда должны иметь число (или шестнадцатеричное число) по обе стороны от десятичной запятой.
Десятичные числа с плавающей запятой также могут иметь необязательный *показатель степени*,
обозначенный заглавной или строчной буквой `e`;
шестнадцатеричные числа с плавающей запятой должны иметь показатель степени,
обозначенный заглавной или строчной буквой `p`.

<!--
  - test: `float-required-vs-optional-exponent-err`

  ```swifttest
  -> let hexWithout = 0x1.5
  !$ error: hexadecimal floating point literal must end with an exponent
  !! let hexWithout = 0x1.5
  !!                       ^
  ```
-->

<!--
  - test: `float-required-vs-optional-exponent`

  ```swifttest
  -> let hexWith = 0x1.5p7
  -> let decimalWithout = 0.5
  -> let decimalWith = 0.5e7
  ```
-->

Для десятичных чисел с показателем степени `x`,
базовое число умножается на 10ˣ:

- `1.25e2` означает 1,25 x 10² или `125.0`.
- `1.25e-2` означает 1,25 x 10⁻² или `0.0125`.

Для шестнадцатеричных чисел с показателем степени `x`,
базовое число умножается на 2ˣ:

- `0xFp2` означает 15 x 2² или `60.0`.
- `0xFp-2` означает 15 x 2⁻² или `3.75`.

Все эти литералы с плавающей запятой имеют десятичное значение `12.1875`:

```swift
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
```

<!--
  - test: `numberLiterals`

  ```swifttest
  -> let decimalDouble = 12.1875
  -> let exponentDouble = 1.21875e1
  -> let hexadecimalDouble = 0xC.3p0
  ```
-->

Числовые литералы могут содержать дополнительное форматирование, чтобы их было легче читать.
Как целые числа, так и числа с плавающей запятой могут быть дополнены дополнительными нулями
и могут содержать символы подчеркивания для повышения читаемости.
Ни один из этих типов форматирования не влияет на базовое значение литерала:

```swift
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
```

<!--
  - test: `numberLiterals`

  ```swifttest
  -> let paddedDouble = 000123.456
  -> let oneMillion = 1_000_000
  -> let justOverOneMillion = 1_000_000.000_000_1
  ```
-->

## Преобразование числовых типов

Используйте тип `Int` для всех целочисленных констант и переменных в вашем коде,
даже если известно, что они неотрицательны.
Использование типа целого числа по умолчанию в повседневных ситуациях означает, что
целочисленные константы и переменные немедленно взаимосовместимы в вашем коде
и будут соответствовать выведенному типу для целочисленных литералов.

Используйте другие целочисленные типы только тогда, когда они действительно необходимы для задачи,
из-за явно определенных данных из внешнего источника,
или для выполнения оптимизации производительности, использования памяти или других необходимых оптимизаций.
Использование явно определенных типов в этих ситуациях
помогает выявить любые случайные переполнения значений
и неявно документирует характер используемых данных.

### Преобразование целых чисел

Диапазон чисел, которые можно хранить в константе или переменной целого типа,
различен для каждого числового типа.
Константа или переменная типа `Int8` может хранить числа от `-128` до `127`,
в то время как константа или переменная типа `UInt8` может хранить числа от `0` до `255`.
Число, которое не помещается в константу или переменную с определенным размером целого числа,
сообщается как ошибка при компиляции вашего кода:

```swift
let cannotBeNegative: UInt8 = -1
// UInt8 не может хранить отрицательные числа, и поэтому это вызовет ошибку
let tooBig: Int8 = Int8.max + 1
// Int8 не может хранить число, превышающее его максимальное значение,
// и поэтому это также вызовет ошибку
```

<!--
  - test: `constantsAndVariablesOverflowError`

  ```swifttest
  -> let cannotBeNegative: UInt8 = -1
  // UInt8 can't store negative numbers, and so this will report an error
  -> let tooBig: Int8 = Int8.max + 1
  // Int8 can't store a number larger than its maximum value,
  // and so this will also report an error
  !! /tmp/swifttest.swift:2:29: error: arithmetic operation '127 + 1' (on type 'Int8') results in an overflow
  !! let tooBig: Int8 = Int8.max + 1
  !!                    ~~~~~~~~ ^ ~
  !! /tmp/swifttest.swift:1:31: error: negative integer '-1' overflows when stored into unsigned type 'UInt8'
  !! let cannotBeNegative: UInt8 = -1
  !!                                ^
  ```
-->

Поскольку каждый числовой тип может хранить различный диапазон значений,
вы должны явно выбирать преобразование числового типа в каждом конкретном случае.
Этот подход предотвращает скрытые ошибки преобразования
и помогает сделать намерения по преобразованию типов явными в вашем коде.

Чтобы преобразовать один конкретный числовой тип в другой,
вы инициализируете новое число нужного типа существующим значением.
В приведенном ниже примере
константа `twoThousand` имеет тип `UInt16`,
тогда как константа `one` имеет тип `UInt8`.
Их нельзя складывать напрямую,
потому что они не одного и того же типа.
Вместо этого в этом примере вызывается `UInt16(one)` для создания
нового `UInt16`, инициализированного значением `one`,
и это значение используется вместо исходного:

```swift
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
```

<!--
  - test: `typeConversion`

  ```swifttest
  -> let twoThousand: UInt16 = 2_000
  -> let one: UInt8 = 1
  -> let twoThousandAndOne = twoThousand + UInt16(one)
  >> print(twoThousandAndOne)
  << 2001
  ```
-->

Поскольку обе стороны сложения теперь имеют тип `UInt16`,
сложение разрешено.
Итоговая константа (`twoThousandAndOne`) выводится как тип `UInt16`,
потому что это сумма двух значений `UInt16`.

`SomeType(ofInitialValue)` - это типичный способ вызова инициализатора типа Swift
и передачи начального значения.
Внутри `UInt16` есть инициализатор, принимающий значение типа `UInt8`,
и поэтому этот инициализатор используется для создания нового `UInt16` из существующего `UInt8`.
Здесь вы не можете передавать *любой* тип, однако ---
это должен быть тип, для которого `UInt16` предоставляет инициализатор.
Расширение существующих типов для предоставления инициализаторов, принимающих новые типы
(включая ваши собственные определения типов)
рассматривается в разделе <doc:Extensions>.

### Integer and Floating-Point Conversion

Conversions between integer and floating-point numeric types must be made explicit:

```swift
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi equals 3.14159, and is inferred to be of type Double
```

<!--
  - test: `typeConversion`

  ```swifttest
  -> let three = 3
  -> let pointOneFourOneFiveNine = 0.14159
  -> let pi = Double(three) + pointOneFourOneFiveNine
  /> pi equals \(pi), and is inferred to be of type Double
  </ pi equals 3.14159, and is inferred to be of type Double
  ```
-->

Here, the value of the constant `three` is used to create a new value of type `Double`,
so that both sides of the addition are of the same type.
Without this conversion in place, the addition would not be allowed.

Floating-point to integer conversion must also be made explicit.
An integer type can be initialized with a `Double` or `Float` value:

```swift
let integerPi = Int(pi)
// integerPi equals 3, and is inferred to be of type Int
```

<!--
  - test: `typeConversion`

  ```swifttest
  -> let integerPi = Int(pi)
  /> integerPi equals \(integerPi), and is inferred to be of type Int
  </ integerPi equals 3, and is inferred to be of type Int
  ```
-->

Floating-point values are always truncated when used to initialize a new integer value in this way.
This means that `4.75` becomes `4`, and `-3.9` becomes `-3`.

> Note: The rules for combining numeric constants and variables are different from
> the rules for numeric literals.
> The literal value `3` can be added directly to the literal value `0.14159`,
> because number literals don't have an explicit type in and of themselves.
> Their type is inferred only at the point that they're evaluated by the compiler.

<!--
  NOTE: this section on explicit conversions could be included in the Operators section.
  I think it's more appropriate here, however,
  and helps to reinforce the “just use Int” message.
-->

## Type Aliases

*Type aliases* define an alternative name for an existing type.
You define type aliases with the `typealias` keyword.

Type aliases are useful when you want to refer to an existing type
by a name that's contextually more appropriate,
such as when working with data of a specific size from an external source:

```swift
typealias AudioSample = UInt16
```

<!--
  - test: `typeAliases`

  ```swifttest
  -> typealias AudioSample = UInt16
  ```
-->

Once you define a type alias,
you can use the alias anywhere you might use the original name:

```swift
var maxAmplitudeFound = AudioSample.min
// maxAmplitudeFound is now 0
```

<!--
  - test: `typeAliases`

  ```swifttest
  -> var maxAmplitudeFound = AudioSample.min
  /> maxAmplitudeFound is now \(maxAmplitudeFound)
  </ maxAmplitudeFound is now 0
  ```
-->

Here, `AudioSample` is defined as an alias for `UInt16`.
Because it's an alias,
the call to `AudioSample.min` actually calls `UInt16.min`,
which provides an initial value of `0` for the `maxAmplitudeFound` variable.

## Booleans

Swift has a basic *Boolean* type, called `Bool`.
Boolean values are referred to as *logical*,
because they can only ever be true or false.
Swift provides two Boolean constant values,
`true` and `false`:

```swift
let orangesAreOrange = true
let turnipsAreDelicious = false
```

<!--
  - test: `booleans`

  ```swifttest
  -> let orangesAreOrange = true
  -> let turnipsAreDelicious = false
  ```
-->

The types of `orangesAreOrange` and `turnipsAreDelicious`
have been inferred as `Bool` from the fact that
they were initialized with Boolean literal values.
As with `Int` and `Double` above,
you don't need to declare constants or variables as `Bool`
if you set them to `true` or `false` as soon as you create them.
Type inference helps make Swift code more concise and readable
when it initializes constants or variables with other values whose type is already known.

Boolean values are particularly useful when you work with conditional statements
such as the `if` statement:

```swift
if turnipsAreDelicious {
    print("Mmm, tasty turnips!")
} else {
    print("Eww, turnips are horrible.")
}
// Prints "Eww, turnips are horrible."
```

<!--
  - test: `booleans`

  ```swifttest
  -> if turnipsAreDelicious {
        print("Mmm, tasty turnips!")
     } else {
        print("Eww, turnips are horrible.")
     }
  <- Eww, turnips are horrible.
  ```
-->

Conditional statements such as the `if` statement are covered in more detail in <doc:ControlFlow>.

Swift's type safety prevents non-Boolean values from being substituted for `Bool`.
The following example reports a compile-time error:

```swift
let i = 1
if i {
    // this example will not compile, and will report an error
}
```

<!--
  - test: `booleansNotBoolean`

  ```swifttest
  -> let i = 1
  -> if i {
        // this example will not compile, and will report an error
     }
  !$ error: type 'Int' cannot be used as a boolean; test for '!= 0' instead
  !! if i {
  !!   ^
  !! ( != 0)
  ```
-->

However, the alternative example below is valid:

```swift
let i = 1
if i == 1 {
    // this example will compile successfully
}
```

<!--
  - test: `booleansIsBoolean`

  ```swifttest
  -> let i = 1
  -> if i == 1 {
        // this example will compile successfully
     }
  ```
-->

The result of the `i == 1` comparison is of type `Bool`,
and so this second example passes the type-check.
Comparisons like `i == 1` are discussed in <doc:BasicOperators>.

As with other examples of type safety in Swift,
this approach avoids accidental errors
and ensures that the intention of a particular section of code is always clear.

## Tuples

*Tuples* group multiple values into a single compound value.
The values within a tuple can be of any type
and don't have to be of the same type as each other.

In this example, `(404, "Not Found")` is a tuple that describes an *HTTP status code*.
An HTTP status code is a special value returned by a web server whenever you request a web page.
A status code of `404 Not Found` is returned if you request a webpage that doesn't exist.

```swift
let http404Error = (404, "Not Found")
// http404Error is of type (Int, String), and equals (404, "Not Found")
```

<!--
  - test: `tuples`

  ```swifttest
  -> let http404Error = (404, "Not Found")
  /> http404Error is of type (Int, String), and equals (\(http404Error.0), \"\(http404Error.1)\")
  </ http404Error is of type (Int, String), and equals (404, "Not Found")
  ```
-->

The `(404, "Not Found")` tuple groups together an `Int` and a `String`
to give the HTTP status code two separate values:
a number and a human-readable description.
It can be described as “a tuple of type `(Int, String)`”.

You can create tuples from any permutation of types,
and they can contain as many different types as you like.
There's nothing stopping you from having
a tuple of type `(Int, Int, Int)`, or `(String, Bool)`,
or indeed any other permutation you require.

You can *decompose* a tuple's contents into separate constants or variables,
which you then access as usual:

```swift
let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")
// Prints "The status code is 404"
print("The status message is \(statusMessage)")
// Prints "The status message is Not Found"
```

<!--
  - test: `tuples`

  ```swifttest
  -> let (statusCode, statusMessage) = http404Error
  -> print("The status code is \(statusCode)")
  <- The status code is 404
  -> print("The status message is \(statusMessage)")
  <- The status message is Not Found
  ```
-->

If you only need some of the tuple's values,
ignore parts of the tuple with an underscore (`_`)
when you decompose the tuple:

```swift
let (justTheStatusCode, _) = http404Error
print("The status code is \(justTheStatusCode)")
// Prints "The status code is 404"
```

<!--
  - test: `tuples`

  ```swifttest
  -> let (justTheStatusCode, _) = http404Error
  -> print("The status code is \(justTheStatusCode)")
  <- The status code is 404
  ```
-->

Alternatively,
access the individual element values in a tuple using index numbers starting at zero:

```swift
print("The status code is \(http404Error.0)")
// Prints "The status code is 404"
print("The status message is \(http404Error.1)")
// Prints "The status message is Not Found"
```

<!--
  - test: `tuples`

  ```swifttest
  -> print("The status code is \(http404Error.0)")
  <- The status code is 404
  -> print("The status message is \(http404Error.1)")
  <- The status message is Not Found
  ```
-->

You can name the individual elements in a tuple when the tuple is defined:

```swift
let http200Status = (statusCode: 200, description: "OK")
```

<!--
  - test: `tuples`

  ```swifttest
  -> let http200Status = (statusCode: 200, description: "OK")
  ```
-->

If you name the elements in a tuple,
you can use the element names to access the values of those elements:

```swift
print("The status code is \(http200Status.statusCode)")
// Prints "The status code is 200"
print("The status message is \(http200Status.description)")
// Prints "The status message is OK"
```

<!--
  - test: `tuples`

  ```swifttest
  -> print("The status code is \(http200Status.statusCode)")
  <- The status code is 200
  -> print("The status message is \(http200Status.description)")
  <- The status message is OK
  ```
-->

Tuples are particularly useful as the return values of functions.
A function that tries to retrieve a web page might return the `(Int, String)` tuple type
to describe the success or failure of the page retrieval.
By returning a tuple with two distinct values,
each of a different type,
the function provides more useful information about its outcome
than if it could only return a single value of a single type.
For more information, see <doc:Functions#Functions-with-Multiple-Return-Values>.

> Note: Tuples are useful for simple groups of related values.
> They're not suited to the creation of complex data structures.
> If your data structure is likely to be more complex,
> model it as a class or structure, rather than as a tuple.
> For more information, see <doc:ClassesAndStructures>.

## Optionals

You use *optionals* in situations where a value may be absent.
An optional represents two possibilities:
Either there *is* a value of a specified type,
and you can unwrap the optional to access that value,
or there *isn't* a value at all.

As an example of a value that might be missing,
Swift's `Int` type has an initializer
that tries to convert a `String` value into an `Int` value.
However, only some strings can be converted into integers.
The string `"123"` can be converted into the numeric value `123`,
but the string `"hello, world"` doesn't have a corresponding numeric value.
The example below uses the initializer to try to convert a `String` into an `Int`:

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
// The type of convertedNumber is "optional Int"
```

<!--
  - test: `optionals`

  ```swifttest
  -> let possibleNumber = "123"
  -> let convertedNumber = Int(possibleNumber)
  // convertedNumber is inferred to be of type "Int?", or "optional Int"
  >> print(type(of: convertedNumber))
  << Optional<Int>
  ```
-->

Because the initializer in the code above might fail,
it returns an *optional* `Int`, rather than an `Int`.

To write an optional type,
you write a question mark (`?`)
after the name of the type that the optional contains ---
for example, the type of an optional `Int` is `Int?`.
An optional `Int` always contains
either some `Int` value or no value at all.
It can't contain anything else, like a `Bool` or `String` value.

### nil

You set an optional variable to a valueless state
by assigning it the special value `nil`:

```swift
var serverResponseCode: Int? = 404
// serverResponseCode contains an actual Int value of 404
serverResponseCode = nil
// serverResponseCode now contains no value
```

<!--
  - test: `optionals`

  ```swifttest
  -> var serverResponseCode: Int? = 404
  /> serverResponseCode contains an actual Int value of \(serverResponseCode!)
  </ serverResponseCode contains an actual Int value of 404
  -> serverResponseCode = nil
  // serverResponseCode now contains no value
  ```
-->

If you define an optional variable without providing a default value,
the variable is automatically set to `nil`:

```swift
var surveyAnswer: String?
// surveyAnswer is automatically set to nil
```

<!--
  - test: `optionals`

  ```swifttest
  -> var surveyAnswer: String?
  // surveyAnswer is automatically set to nil
  ```
-->

You can use an `if` statement to find out whether an optional contains a value
by comparing the optional against `nil`.
You perform this comparison with the “equal to” operator (`==`)
or the “not equal to” operator (`!=`).

If an optional has a value, it's considered as “not equal to” `nil`:

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)

if convertedNumber != nil {
    print("convertedNumber contains some integer value.")
}
// Prints "convertedNumber contains some integer value."
```

<!--
  - test: `optionals`

  ```swifttest
  -> if convertedNumber != nil {
        print("convertedNumber contains some integer value.")
     }
  <- convertedNumber contains some integer value.
  ```
-->

You can't use `nil` with non-optional constants or variables.
If a constant or variable in your code needs to work with
the absence of a value under certain conditions,
declare it as an optional value of the appropriate type.
A constant or variable that's declared as a non-optional value
is guaranteed to never contain a `nil` value.
If you try to assign `nil` to a non-optional value,
you'll get a compile-time error.

This separation of optional and non-optional values
lets you explicitly mark what information can be missing,
and makes it easier to write code that handle missing values.
You can't accidentally treat an optional as if it were non-optional
because this mistake produces an error at compile time.
After you unwrap the value,
none of the other code that works with that value needs to check for `nil`,
so there's no need to repeatedly check the same value
in different parts of your code.

When you access an optional value,
your code always handles both the `nil` and non-`nil` case.
There are several things you can do when a value is missing,
as described in the following sections:

- Skip the code that operates on the value when it's `nil`.

- Propagate the `nil` value,
  by returning `nil`
  or using the `?.` operator described in <doc:OptionalChaining>.

- Provide a fallback value, using the `??` operator.

- Stop program execution, using the `!` operator.

> Note:
> In Objective-C, `nil` is a pointer to a nonexistent object.
> In Swift, `nil` isn't a pointer --- it's the absence of a value of a certain type.
> Optionals of *any* type can be set to `nil`, not just object types.

### Optional Binding

You use optional binding to find out whether an optional contains a value,
and if so, to make that value available as a temporary constant or variable.
Optional binding can be used with `if`, `guard`, and `while` statements
to check for a value inside an optional,
and to extract that value into a constant or variable,
as part of a single action.
For more information about `if`, `guard`, and `while` statements,
see <doc:ControlFlow>.

Write an optional binding for an `if` statement as follows:

```swift
if let <#constantName#> = <#someOptional#> {
   <#statements#>
}
```

You can rewrite the `possibleNumber` example from
the <doc:TheBasics#Optionals> section
to use optional binding rather than forced unwrapping:

```swift
if let actualNumber = Int(possibleNumber) {
    print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
    print("The string \"\(possibleNumber)\" couldn't be converted to an integer")
}
// Prints "The string "123" has an integer value of 123"
```

<!--
  - test: `optionals`

  ```swifttest
  -> if let actualNumber = Int(possibleNumber) {
        print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
     } else {
        print("The string \"\(possibleNumber)\" couldn't be converted to an integer")
     }
  <- The string "123" has an integer value of 123
  ```
-->

This code can be read as:

“If the optional `Int` returned by `Int(possibleNumber)` contains a value,
set a new constant called `actualNumber` to the value contained in the optional.”

If the conversion is successful,
the `actualNumber` constant becomes available for use within
the first branch of the `if` statement.
It has already been initialized with the value contained within the optional,
and has the corresponding non-optional type.
In this case, the type of `possibleNumber` is `Int?`,
so the type of `actualNumber` is `Int`.

If you don't need to refer to the original, optional constant or variable
after accessing the value it contains,
you can use the same name for the new constant or variable:

```swift
let myNumber = Int(possibleNumber)
// Here, myNumber is an optional integer
if let myNumber = myNumber {
    // Here, myNumber is a non-optional integer
    print("My number is \(myNumber)")
}
// Prints "My number is 123"
```

<!--
  - test: `optionals`

  ```swifttest
  -> let myNumber = Int(possibleNumber)
  // Here, myNumber is an optional integer
  -> if let myNumber = myNumber {
         // Here, myNumber is a non-optional integer
         print("My number is \(myNumber)")
     }
  <- My number is 123
  ```
-->

This code starts by checking whether `myNumber` contains a value,
just like the code in the previous example.
If `myNumber` has a value,
the value of a new constant named `myNumber` is set to that value.
Inside the body of the `if` statement,
writing `myNumber` refers to that new non-optional constant.
Writing `myNumber` before or after the `if` statement
refers to the original optional integer constant.

Because this kind of code is so common,
you can use a shorter spelling to unwrap an optional value:
Write just the name of the constant or variable that you're unwrapping.
The new, unwrapped constant or variable
implicitly uses the same name as the optional value.

```swift
if let myNumber {
    print("My number is \(myNumber)")
}
// Prints "My number is 123"
```

<!--
  - test: `optionals`

  ```swifttest
  -> if let myNumber {
         print("My number is \(myNumber)")
     }
  <- My number is 123
  ```
-->

You can use both constants and variables with optional binding.
If you wanted to manipulate the value of `myNumber`
within the first branch of the `if` statement,
you could write `if var myNumber` instead,
and the value contained within the optional
would be made available as a variable rather than a constant.
Changes you make to `myNumber` inside the body of the `if` statement
apply only to that local variable,
*not* to the original, optional constant or variable that you unwrapped.

You can include as many optional bindings and Boolean conditions
in a single `if` statement as you need to,
separated by commas.
If any of the values in the optional bindings are `nil`
or any Boolean condition evaluates to `false`,
the whole `if` statement's condition
is considered to be `false`.
The following `if` statements are equivalent:

```swift
if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
    print("\(firstNumber) < \(secondNumber) < 100")
}
// Prints "4 < 42 < 100"

if let firstNumber = Int("4") {
    if let secondNumber = Int("42") {
        if firstNumber < secondNumber && secondNumber < 100 {
            print("\(firstNumber) < \(secondNumber) < 100")
        }
    }
}
// Prints "4 < 42 < 100"
```

<!--
  - test: `multipleOptionalBindings`

  ```swifttest
  -> if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
        print("\(firstNumber) < \(secondNumber) < 100")
     }
  <- 4 < 42 < 100
  ---
  -> if let firstNumber = Int("4") {
         if let secondNumber = Int("42") {
             if firstNumber < secondNumber && secondNumber < 100 {
                 print("\(firstNumber) < \(secondNumber) < 100")
             }
         }
     }
  <- 4 < 42 < 100
  ```
-->

<!--
  The example above uses multiple optional bindings
  to show that you can have more than one
  and to show the short-circuiting behavior.
  It has multiple Boolean conditions
  to show that you should join logically related conditions
  using the && operator instead of a comma.
-->

Constants and variables created with optional binding in an `if` statement
are available only within the body of the `if` statement.
In contrast, the constants and variables created with a `guard` statement
are available in the lines of code that follow the `guard` statement,
as described in <doc:ControlFlow#Early-Exit>.

### Providing a Fallback Value

Another way to handle a missing value is to supply
a default value using the nil-coalescing operator (`??`).
If the optional on the left of the `??` isn't `nil`,
that value is unwrapped and used.
Otherwise, the value on the right of `??` is used.
For example,
the code below greets someone by name if one is specified,
and uses a generic greeting when the name is `nil`.

```swift
let name: String? = nil
let greeting = "Hello, " + (name ?? "friend") + "!"
print(greeting)
// Prints "Hello, friend!"
```

<!--
.. testcode:: optionalFallback

   ```swifttest
   -> let name: String? = nil
   -> let greeting = "Hello, " + (name ?? "friend") + "!"
   -> print(greeting)
   <- Hello, friend!
   ```
-->

For more information about using `??` to provide a fallback value,
see <doc:BasicOperators#Nil-Coalescing-Operator>.

### Force Unwrapping

When `nil` represents an unrecoverable failure,
such as a programmer error or corrupted state,
you can access the underlying value
by adding an exclamation mark (`!`) to the end of the optional's name.
This is known as *force unwrapping* the optional's value.
When you force unwrap a non-`nil` value,
the result is its unwrapped value.
Force unwrapping a `nil` value triggers a runtime error.

The `!` is, effectively, a shorter spelling of [`fatalError(_:file:line:)`][].
For example, the code below shows two equivalent approaches:

[`fatalError(_:file:line:)`]: https://developer.apple.com/documentation/swift/fatalerror(_:file:line:)

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)

let number = convertedNumber!

guard let number = convertedNumber else {
    fatalError("The number was invalid")
}
```

Both versions of the code above depend on `convertedNumber`
always containing a value.
Writing that requirement as part of the code,
using either of the approaches above,
lets your code check that the requirement is true at runtime.

For more information about enforcing data requirements
and checking assumptions at runtime,
see <doc:TheBasics#Assertions-and-Preconditions>.

### Implicitly Unwrapped Optionals

As described above,
optionals indicate that a constant or variable is allowed to have “no value”.
Optionals can be checked with an `if` statement to see if a value exists,
and can be conditionally unwrapped with optional binding
to access the optional's value if it does exist.

Sometimes it's clear from a program's structure that an optional will *always* have a value,
after that value is first set.
In these cases, it's useful to remove the need
to check and unwrap the optional's value every time it's accessed,
because it can be safely assumed to have a value all of the time.

These kinds of optionals are defined as *implicitly unwrapped optionals*.
You write an implicitly unwrapped optional by placing an exclamation point (`String!`)
rather than a question mark (`String?`) after the type that you want to make optional.
Rather than placing an exclamation point after the optional's name when you use it,
you place an exclamation point after the optional's type when you declare it.

Implicitly unwrapped optionals are useful when
an optional's value is confirmed to exist immediately after the optional is first defined
and can definitely be assumed to exist at every point thereafter.
The primary use of implicitly unwrapped optionals in Swift is during class initialization,
as described in <doc:AutomaticReferenceCounting#Unowned-References-and-Implicitly-Unwrapped-Optional-Properties>.

Don't use an implicitly unwrapped optional when there's a possibility of
a variable becoming `nil` at a later point.
Always use a normal optional type if you need to check for a `nil` value
during the lifetime of a variable.

An implicitly unwrapped optional is a normal optional behind the scenes,
but can also be used like a non-optional value,
without the need to unwrap the optional value each time it's accessed.
The following example shows the difference in behavior between
an optional string and an implicitly unwrapped optional string
when accessing their wrapped value as an explicit `String`:

```swift
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // Requires explicit unwrapping

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString // Unwrapped automatically
```

<!--
  - test: `implicitlyUnwrappedOptionals`

  ```swifttest
  -> let possibleString: String? = "An optional string."
  -> let forcedString: String = possibleString! // requires an exclamation point
  ---
  -> let assumedString: String! = "An implicitly unwrapped optional string."
  -> let implicitString: String = assumedString // no need for an exclamation point
  ```
-->

You can think of an implicitly unwrapped optional as
giving permission for the optional to be force-unwrapped if needed.
When you use an implicitly unwrapped optional value,
Swift first tries to use it as an ordinary optional value;
if it can't be used as an optional, Swift force-unwraps the value.
In the code above,
the optional value `assumedString` is force-unwrapped
before assigning its value to `implicitString`
because `implicitString` has an explicit, non-optional type of `String`.
In code below,
`optionalString` doesn't have an explicit type
so it's an ordinary optional.

```swift
let optionalString = assumedString
// The type of optionalString is "String?" and assumedString isn't force-unwrapped.
```

<!--
  - test: `implicitlyUnwrappedOptionals`

  ```swifttest
  -> let optionalString = assumedString
  // The type of optionalString is "String?" and assumedString isn't force-unwrapped.
  >> print(type(of: optionalString))
  << Optional<String>
  ```
-->

If an implicitly unwrapped optional is `nil` and you try to access its wrapped value,
you'll trigger a runtime error.
The result is exactly the same as if you write an exclamation point
to force unwrap a normal optional that doesn't contain a value.

You can check whether an implicitly unwrapped optional is `nil`
the same way you check a normal optional:

```swift
if assumedString != nil {
    print(assumedString!)
}
// Prints "An implicitly unwrapped optional string."
```

<!--
  - test: `implicitlyUnwrappedOptionals`

  ```swifttest
  -> if assumedString != nil {
        print(assumedString!)
     }
  <- An implicitly unwrapped optional string.
  ```
-->

You can also use an implicitly unwrapped optional with optional binding,
to check and unwrap its value in a single statement:

```swift
if let definiteString = assumedString {
    print(definiteString)
}
// Prints "An implicitly unwrapped optional string."
```

<!--
  - test: `implicitlyUnwrappedOptionals`

  ```swifttest
  -> if let definiteString = assumedString {
        print(definiteString)
     }
  <- An implicitly unwrapped optional string.
  ```
-->

## Error Handling

You use *error handling* to respond to error conditions
your program may encounter during execution.

In contrast to optionals,
which can use the presence or absence of a value
to communicate success or failure of a function,
error handling allows you to determine the underlying cause of failure,
and, if necessary, propagate the error to another part of your program.

When a function encounters an error condition, it *throws* an error.
That function's caller can then *catch* the error and respond appropriately.

```swift
func canThrowAnError() throws {
    // this function may or may not throw an error
}
```

<!--
  - test: `errorHandling`

  ```swifttest
  >> enum SimpleError: Error {
  >>    case someError
  >> }
  >> let condition = true
  -> func canThrowAnError() throws {
        // this function may or may not throw an error
  >>    if condition {
  >>       throw SimpleError.someError
  >>    }
     }
  ```
-->

A function indicates that it can throw an error
by including the `throws` keyword in its declaration.
When you call a function that can throw an error,
you prepend the `try` keyword to the expression.

Swift automatically propagates errors out of their current scope
until they're handled by a `catch` clause.

```swift
do {
    try canThrowAnError()
    // no error was thrown
} catch {
    // an error was thrown
}
```

<!--
  - test: `errorHandling`

  ```swifttest
  -> do {
  ->    try canThrowAnError()
  >>    print("No Error")
  ->    // no error was thrown
  -> } catch {
  >>    print("Error")
  ->    // an error was thrown
  -> }
  << Error
  ```
-->

A `do` statement creates a new containing scope,
which allows errors to be propagated to one or more `catch` clauses.

Here's an example of how error handling can be used
to respond to different error conditions:

```swift
func makeASandwich() throws {
    // ...
}

do {
    try makeASandwich()
    eatASandwich()
} catch SandwichError.outOfCleanDishes {
    washDishes()
} catch SandwichError.missingIngredients(let ingredients) {
    buyGroceries(ingredients)
}
```

<!--
  - test: `errorHandlingTwo`

  ```swifttest
  >> enum SandwichError: Error {
  >>     case outOfCleanDishes
  >>     case missingIngredients([String])
  >> }
  >> func washDishes() { print("Wash dishes") }
  >> func buyGroceries(_ shoppingList: [String]) { print("Buy \(shoppingList)") }
  -> func makeASandwich() throws {
         // ...
     }
  >> func eatASandwich() {}
  ---
  -> do {
         try makeASandwich()
         eatASandwich()
     } catch SandwichError.outOfCleanDishes {
         washDishes()
     } catch SandwichError.missingIngredients(let ingredients) {
         buyGroceries(ingredients)
     }
  ```
-->

In this example, the `makeASandwich()` function will throw an error
if no clean dishes are available
or if any ingredients are missing.
Because `makeASandwich()` can throw an error,
the function call is wrapped in a `try` expression.
By wrapping the function call in a `do` statement,
any errors that are thrown will be propagated
to the provided `catch` clauses.

If no error is thrown, the `eatASandwich()` function is called.
If an error is thrown and it matches the `SandwichError.outOfCleanDishes` case,
then the `washDishes()` function will be called.
If an error is thrown and it matches the `SandwichError.missingIngredients` case,
then the `buyGroceries(_:)` function is called
with the associated `[String]` value captured by the `catch` pattern.

Throwing, catching, and propagating errors is covered in greater detail in
<doc:ErrorHandling>.

## Assertions and Preconditions

*Assertions* and *preconditions*
are checks that happen at runtime.
You use them to make sure an essential condition is satisfied
before executing any further code.
If the Boolean condition in the assertion or precondition
evaluates to `true`,
code execution continues as usual.
If the condition evaluates to `false`,
the current state of the program is invalid;
code execution ends, and your app is terminated.

You use assertions and preconditions
to express the assumptions you make
and the expectations you have
while coding,
so you can include them as part of your code.
Assertions help you find mistakes and incorrect assumptions during development,
and preconditions help you detect issues in production.

In addition to verifying your expectations at runtime,
assertions and preconditions also become a useful form of documentation
within the code.
Unlike the error conditions discussed in <doc:TheBasics#Error-Handling> above,
assertions and preconditions aren't used
for recoverable or expected errors.
Because a failed assertion or precondition
indicates an invalid program state,
there's no way to catch a failed assertion.
Recovering from an invalid state is impossible.
When an assertion fails,
at least one piece of the program's data is invalid ---
but you don't know why it's invalid
or whether an additional state is also invalid.

Using assertions and preconditions
isn't a substitute for designing your code in such a way
that invalid conditions are unlikely to arise.
However,
using them to enforce valid data and state
causes your app to terminate more predictably
if an invalid state occurs,
and helps make the problem easier to debug.
When assumptions aren't checked,
you might not notice this kind problem until much later
when code elsewhere starts failing visibly,
and after user data has been silently corrupted.
Stopping execution as soon as an invalid state is detected
also helps limit the damage caused by that invalid state.

The difference between assertions and preconditions is in when they're checked:
Assertions are checked only in debug builds,
but preconditions are checked in both debug and production builds.
In production builds,
the condition inside an assertion isn't evaluated.
This means you can use as many assertions as you want
during your development process,
without impacting performance in production.

### Debugging with Assertions

<!--
  If your code triggers an assertion while running in a debug environment,
  such as when you build and run an app in Xcode,
  you can see exactly where the invalid state occurred
  and query the state of your app at the time that the assertion was triggered.
  An assertion also lets you provide a suitable debug message as to the nature of the assert.
-->

You write an assertion by calling the
[`assert(_:_:file:line:)`](https://developer.apple.com/documentation/swift/1541112-assert) function
from the Swift standard library.
You pass this function an expression that evaluates to `true` or `false`
and a message to display if the result of the condition is `false`.
For example:

```swift
let age = -3
assert(age >= 0, "A person's age can't be less than zero.")
// This assertion fails because -3 isn't >= 0.
```

<!--
  - test: `assertions-1`

  ```swifttest
  -> let age = -3
  -> assert(age >= 0, "A person's age can't be less than zero.")
  xx assert
  // This assertion fails because -3 isn't >= 0.
  ```
-->

In this example, code execution continues if `age >= 0` evaluates to `true`,
that is, if the value of `age` is nonnegative.
If the value of `age` is negative, as in the code above,
then `age >= 0` evaluates to `false`,
and the assertion fails, terminating the application.

You can omit the assertion message ---
for example, when it would just repeat the condition as prose.

```swift
assert(age >= 0)
```

<!--
  - test: `assertions-2`

  ```swifttest
  >> let age = -3
  -> assert(age >= 0)
  xx assert
  ```
-->

<!--
  - test: `assertionsCanUseStringInterpolation`

  ```swifttest
  -> let age = -3
  -> assert(age >= 0, "A person's age can't be less than zero, but value is \(age).")
  xx assert
  ```
-->

If the code already checks the condition,
you use the
[`assertionFailure(_:file:line:)`](https://developer.apple.com/documentation/swift/1539616-assertionfailure) function
to indicate that an assertion has failed.
For example:

```swift
if age > 10 {
    print("You can ride the roller-coaster or the ferris wheel.")
} else if age >= 0 {
    print("You can ride the ferris wheel.")
} else {
    assertionFailure("A person's age can't be less than zero.")
}
```

<!--
  - test: `assertions-3`

  ```swifttest
  >> let age = -3
  -> if age > 10 {
         print("You can ride the roller-coaster or the ferris wheel.")
     } else if age >= 0 {
         print("You can ride the ferris wheel.")
     } else {
         assertionFailure("A person's age can't be less than zero.")
     }
  xx assert
  ```
-->

### Enforcing Preconditions

Use a precondition whenever a condition has the potential to be false,
but must *definitely* be true for your code to continue execution.
For example, use a precondition to check that a subscript isn't out of bounds,
or to check that a function has been passed a valid value.

You write a precondition by calling the
[`precondition(_:_:file:line:)`](https://developer.apple.com/documentation/swift/1540960-precondition) function.
You pass this function an expression that evaluates to `true` or `false`
and a message to display if the result of the condition is `false`.
For example:

```swift
// In the implementation of a subscript...
precondition(index > 0, "Index must be greater than zero.")
```

<!--
  - test: `preconditions`

  ```swifttest
  >> let index = -1
  // In the implementation of a subscript...
  -> precondition(index > 0, "Index must be greater than zero.")
  xx assert
  ```
-->

You can also call the
[`preconditionFailure(_:file:line:)`](https://developer.apple.com/documentation/swift/1539374-preconditionfailure) function
to indicate that a failure has occurred ---
for example, if the default case of a switch was taken,
but all valid input data should have been handled
by one of the switch's other cases.

> Note: If you compile in unchecked mode (`-Ounchecked`),
> preconditions aren't checked.
> The compiler assumes that preconditions are always true,
> and it optimizes your code accordingly.
> However, the `fatalError(_:file:line:)` function always halts execution,
> regardless of optimization settings.
>
> You can use the `fatalError(_:file:line:)` function
> during prototyping and early development
> to create stubs for functionality that hasn't been implemented yet,
> by writing `fatalError("Unimplemented")` as the stub implementation.
> Because fatal errors are never optimized out,
> unlike assertions or preconditions,
> you can be sure that execution always halts
> if it encounters a stub implementation.

<!--
  "\ " in the first cell below lets it be empty.
  Otherwise RST treats the row as a continuation.

  ============ =====  ==========  ===============================
  \            Debug  Production  Production with ``-Ounchecked``
  ============ =====  ==========  ===============================
  Assertion    Yes    No          No
  ------------ -----  ----------  -------------------------------
  Precondition Yes    Yes         No
  ------------ -----  ----------  -------------------------------
  Fatal Error  Yes    Yes         Yes
  ============ =====  ==========  ===============================
-->

<!--
  TODO: In Xcode, can you set a breakpoint on assertion/precondition failure?
  If so, mention that fact and give a link to a guide that shows you how.
  In LLDB, 'breakpoint set -E swift' catches when errors are thrown,
  but doesn't stop at assertions.
-->

<!--
This source file is part of the Swift.org open source project

Copyright (c) 2014 - 2022 Apple Inc. and the Swift project authors
Licensed under Apache License v2.0 with Runtime Library Exception

See https://swift.org/LICENSE.txt for license information
See https://swift.org/CONTRIBUTORS.txt for the list of Swift project authors
-->
