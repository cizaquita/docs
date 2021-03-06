Руководство по совместимости
############################

Мы обеспечиваем то, чтобы вы могли легко и плавно обновлять свои приложения.
Вот почему мы нарушаем совместимость на основных этапах релиза.
Вы можете быть знакомы с `семантическим версированием <https://semver.org/lang/ru/>`_,
это общее руководство, которое мы используем для всех проектов CakePHP. Короче говоря, семантическое
управление версиями означает, что только основные выпуски (например, 2.0, 3.0, 4.0) могут иметь
обратную совместимость. Незначительные релизы ('Minor releases')(например, 2.1, 3.1, 3.2),
добавляющие функциональность, могут нарушать обратную совместимость. Исправления ошибок
('Bug fix releases')(например, 2.1.2, 3.0.1) не добавляют новых функций, но исправляют
ошибки или повышают производительность.

.. note::

	Устаревшее ('Deprecations') удаляется со следующей основной версией фреймворка.
	Вам рекомендуется на раннем этапе адаптировать ваш код уже к каждому незначительному
	релизу, как указано в комментарии к устареванию и руководстве по миграции.

Чтобы уточнить, какие изменения вы можете ожидать в каждом следующем выпуске, мы публикуем множнество
подробной информации для разработчиков, использующих CakePHP, а также для разработчиков, работающих над
CakePHP. Она помогает оправдать ожидания того, что можно сделать в небольших выпусках. Главные
релизы ('Major releases') будут иметь наибольшее число изменений.

Руководства по миграции
=======================

Для каждого крупного и мелкого выпуска команда CakePHP обеспечивает руководство
по миграции. Эти руководства объясняют новые функции и любые нарушения, которые
есть в каждом выпуске. Их можно найти в разделе :doc:`/appendices`.

Использование CakePHP
=====================

Если вы создаёте своё приложение с помощью CakePHP, следующие рекомендации
объяснят стабильность, которую вы можете ожидать.

Интерфейсы
----------

Вне основных выпусков ('мajor releases'), интерфейсы предоставляемые CakePHP, **не** будут содержать
существенно изменившиеся методы. Могут быть добавлены новые методы, но никакие существующие методы
не будут изменен.

Классы
------

Классы, предоставляемые CakePHP, могут быть построены и иметь свои общедоступные методы и
свойства, используемые кодом приложения и вне основных выпусков, обеспечивая обратную
совместимость.

.. note::

	Некоторые классы в CakePHP помечены тегом API doc ``@internal``. Эти
	классы **не являются** стабильными и не имеют обещаний обратной совместимости.

В небольших выпусках, могут быть добавлены новые классы, а в существующие методы могут
быть добавлены новые аргументы. Любые новые аргументы будут иметь значения по умолчанию,
но если вы переопределили методы с другой подписью(сигнатурой), это можете вызвать
фатальные ошибки. Методы добавления новых аргументов будут описаны в руководстве по миграции
для этой версии.

В следующей таблице приведены несколько вариантов использования и какую совместимость вы можете
ожидать от CakePHP:

+-------------------------------+--------------------------+
| If you...                     | Backwards compatibility? |
+===============================+==========================+
| Typehint against the class    | Yes                      |
+-------------------------------+--------------------------+
| Create a new instance         | Yes                      |
+-------------------------------+--------------------------+
| Extend the class              | Yes                      |
+-------------------------------+--------------------------+
| Access a public property      | Yes                      |
+-------------------------------+--------------------------+
| Call a public method          | Yes                      |
+-------------------------------+--------------------------+
| **Extend a class and...**                                |
+-------------------------------+--------------------------+
| Override a public property    | Yes                      |
+-------------------------------+--------------------------+
| Access a protected property   | No [1]_                  |
+-------------------------------+--------------------------+
| Override a protected property | No [1]_                  |
+-------------------------------+--------------------------+
| Override a protected method   | No [1]_                  |
+-------------------------------+--------------------------+
| Call a protected method       | No [1]_                  |
+-------------------------------+--------------------------+
| Add a public property         | No                       |
+-------------------------------+--------------------------+
| Add a public method           | No                       |
+-------------------------------+--------------------------+
| Add an argument               | No [1]_                  |
| to an overridden method       |                          |
+-------------------------------+--------------------------+
| Add a default argument value  | Yes                      |
| to an existing method         |                          |
| argument                      |                          |
+-------------------------------+--------------------------+

Работающим над CakePHP
======================

Если вы помогаете сделать CakePHP еще лучше, соблюдайте следующие рекомендации
при добавлении/изменении функциональности:

В незначительном выпуске вы можете:

+-------------------------------+--------------------------+
| In a minor release can you...                            |
+===============================+==========================+
| **Classes**                                              |
+-------------------------------+--------------------------+
| Remove a class                | No                       |
+-------------------------------+--------------------------+
| Remove an interface           | No                       |
+-------------------------------+--------------------------+
| Remove a trait                | No                       |
+-------------------------------+--------------------------+
| Make final                    | No                       |
+-------------------------------+--------------------------+
| Make abstract                 | No                       |
+-------------------------------+--------------------------+
| Change name                   | Yes [2]_                 |
+-------------------------------+--------------------------+
| **Properties**                                           |
+-------------------------------+--------------------------+
| Add a public property         | Yes                      |
+-------------------------------+--------------------------+
| Remove a public property      | No                       |
+-------------------------------+--------------------------+
| Add a protected property      | Yes                      |
+-------------------------------+--------------------------+
| Remove a protected property   | Yes [3]_                 |
+-------------------------------+--------------------------+
| **Methods**                                              |
+-------------------------------+--------------------------+
| Add a public method           | Yes                      |
+-------------------------------+--------------------------+
| Remove a public method        | No                       |
+-------------------------------+--------------------------+
| Add a protected method        | Yes                      |
+-------------------------------+--------------------------+
| Move to parent class          | Yes                      |
+-------------------------------+--------------------------+
| Remove a protected method     | Yes [3]_                 |
+-------------------------------+--------------------------+
| Reduce visibility             | No                       |
+-------------------------------+--------------------------+
| Change method name            | Yes [2]_                 |
+-------------------------------+--------------------------+
| Add a new argument with       | Yes                      |
| default value                 |                          |
+-------------------------------+--------------------------+
| Add a new required argument   | No                       |
| to an existing method.        |                          |
+-------------------------------+--------------------------+
| Remove a default value from   | No                       |
| an existing argument          |                          |
+-------------------------------+--------------------------+
| Change method type void       | Yes                      |
+-------------------------------+--------------------------+

.. [1] Ваш код *может* быть нарушен небольшими выпусками. Проверьте руководство по миграции
	   для уточнения деталей.
.. [2] Вы можете изменить имя класса/метода, пока остаётся его прежнее имя.
	   Этого обычно избегают, если переименование не имеет значительной выгоды.
.. [3] Избегайте, когда это возможно. Любые удаления должны быть задокументированы в руководство по миграции.

Устаревшее
==========

В каждом незначительном выпуске функции могут быть устаревшими. Если функции устарели,
будет добавлена документация API и предупреждения времени выполнения. Ошибки выполнения помогают вам
найти код, который необходимо обновить до его 'смерти'. Если вы захотите отключить ошибки времени выполнения,
вы можете сделать это с помощью конфигурации ``Error.errorLevel``::

    // in config/app.php
    // ...
    'Error' => [
        'errorLevel' => E_ALL ^ E_USER_DEPRECATED,
    ]
    // ...

Отключит предупреждения об устаревании во время выполнения.

