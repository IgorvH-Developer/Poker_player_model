# Проект в разработке.

# Решение задач методами машинного обучения в среде с неполной информацией на примере игры в покер.

### Исследуемая задача.
Цель исследования: изучить и использовать методы машинного обучения в среде с неполной информацией для разработки модели, способной выбирать наиболее выгодные решения. Примером среде с неполной информацией является игра с нулевой суммой – покер.

Проблемы: главная проблема, ложащаяся на плечи искусственного интеллекта – это обработка огромного количества данных и игровых ситуаций.
Используемые методы: среда разработки – Colaboratory и Jupyter Notebook, язык программирования – Python, для построения модели использовались нейронные сети, состоящие из полносвязных слоёв, сети строились с использованием библиотеки Keras.

Возможные применения: алгоритмы, используемые для игры в покер, универсальны и в основном направлены на обучение агентов в средах с неполной информацией, поэтому эти алгоритмы можно перенести на множество приложений, где требуется принятие решений в среде с неполной информацией: как например в безопасности так и в маркетинге.

### Абстракция для неполной информации.
В безлимитном техасском холдеме слишком много моментов для принятия решений, чтобы рассуждать о них по отдельности. Чтобы уменьшить сложность игры исключаются некоторые действия из рассмотрения, а также объединяются похожие точки принятия решений в процессе, это и называется абстракцией в покере. После абстрагирования распределенные точки принятия решения рассматриваются как идентичные. 
В проекте рассматриваются два вида абстракции: абстракция действия и абстракция информации.
I.	Абстракция действия
Абстракция действий уменьшает количество различных действий которые ИИ должен учитывать. В безлимитном техасском холдеме можно сделать любую ставку от 1 BB (большого блайнда) до всех фишек у игрока. Чтобы уменьшить сложность формирования стратегии модель рассматривает только, несколько различных вариантов торговли. 
Три варианта торговли на любой стадии:
•	Сброс карт (Fold)
•	Чек/Колл (check/call; check – продолжаем играть без повышения ставки, при этом никто не делал ставку до; call – уравниваем ставку сделанную, да нашего хода)
•	Бет/Рейз (Bet/Raise; bet – повышение ставки, при этом никто не делал ставку до; raise – переповышение ставки, сделанной до)
II.	Абстракция информации
Другая форма абстракции, которая используется в проекте - это абстракция информации. При такой форме абстракции схожие точки принятия решения объединяются и обрабатываются одинаково. Эти объединённые наборы информации собираются вместе обрабатываются моделью одинаково, тем самым уменьшая количество различных игровых ситуаций. Для обобщения информации вводятся некоторые параметры, характеризующие её. Ниже приведён их список:
•	Сила руки (Hand strength/HS) – используется на последних 3 стадиях торговли (флоп, тёрн, ривер), значение HS лежит в диапазоне [0, 1] и отражает отношение между количеством частных карт другого игрока, которые слабее наших, на общее количество всевозможных частных карт другого игрока.
•	Диаграмма силы руки [3] – диаграмма отражает с какой вероятностью на выбранной стадии выбранная рука будет иметь определённую силу.
Пример некоторых параметров характеризующие стратегию игрока:
•	VPIP – диапазон значений [0, 1], используется на первой стадии игры, описывает отношение между количеством раздач, в которых игрок внёс фишки в игру, и общим количеством раздач.
•	PFR – диапазон значений [0, 1], используется на первой стадии игры, описывает отношение между количеством раздач, в которых игрок повысил ставку, и общим количеством раздач.
•	AF – диапазон значений [0, 1], используется на последних трёх стадиях игры, описывает отношение между количеством раздач, в которых игрок повысил ставку (bet или raise), и общим количеством раздач.
