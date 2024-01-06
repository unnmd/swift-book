# The Swift Programming Language book [Русская версия]

Этот репозиторий содержит исходный код для *The Swift Programming Language book*
(иногда сокращенно как TSPL),
который публикуется на [docs.swift.org.ru][published](в процессе) 
и создается с использованием [Swift-DocC][docc].

## Вклад

Для небольших изменений,
таких как исправление опечаток и изменение нескольких абзацев,
сделайте форк этого репозитория и предложите pull request.

Формальный процесс внесения вклада в этот документ все еще находится в разработке.
Тем временем начните обсуждение в [форумах Swift][forum] для более крупных изменений,
чтобы обсудить свой подход и выявить возможные проблемы
перед тем, как вложить много времени в написание.

Содержание в этой книге следует [Руководству по стилю Apple][asg]
и [стилю этой книги][tspl-style].

Сообщайте о проблемах с содержанием на [странице проблем][bugs] на GitHub.

Обсуждения и вклады следуют [Кодексу поведения Swift][conduct].

Дополнительную информацию смотрите в разделе [Внесение вклада в Язык программирования Swift][contributing].

[asg]: https://help.apple.com/applestyleguide/
[bugs]: https://github.com/unnmd/swift-book/issues
[conduct]: https://www.swift.org/code-of-conduct
[contributing]: /CONTRIBUTING.md
[forum]: https://forums.swift.org/c/swift-documentation/92
[tspl-style]: /Style.md
[published]: https://docs.swift.org.ru/swift-book/documentation/the-swift-programming-language/
[docc]: https://github.com/apple/swift-docc

## Сборка

Запустите `docc preview TSPL.docc`
в корневом каталоге этого репозитория.

После запуска DocC откройте ссылку, которую выводит `docc`,
чтобы отобразить локальный просмотр в вашем браузере.

> Примечание:
>
> Если вы установили DocC, загрузив набор инструментов с Swift.org,
> `docc` находится в каталоге `usr/bin/`,
> относительно установочного пути набора инструментов.
> Убедитесь, что переменная среды `PATH` вашего оболочки
> включает этот каталог.
>
> Если вы установили DocC, загрузив Xcode,
> запустите вместо этого `xcrun docc preview TSPL.docc`.
