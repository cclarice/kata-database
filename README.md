# Kata Notepad 📓

## Первое ревью:

### Вопросы

* Что такое специфичность в css? как работает расчет специфичности?
* Какие есть проблемы в верстке инлайн-блоками?
* БЭМ - что такое блок, элемент, модификатор, микс?
* Относительно чего задается позиционирование?
* Какие свойства создают контекст наложения? Прочитать про контекст наложения
* Что такое babel и для чего нужен?
* Что такое source map?

| Вопрос, ссылка на мой ответ | Ресурсы |
|-----------------------------|---------|
| [CSS спецефичность](#answer_css_specificity) | [Специфичность MDN Web Docs](https://developer.mozilla.org/ru/docs/Web/CSS/Specificity#%D0%BA%D0%B0%D0%BA_%D0%B2%D1%8B%D1%87%D0%B8%D1%81%D0%BB%D1%8F%D0%B5%D1%82%D1%81%D1%8F_%D1%81%D0%BF%D0%B5%D1%86%D0%B8%D1%84%D0%B8%D1%87%D0%BD%D0%BE%D1%81%D1%82%D1%8C) |
| [Inline блоки](#answer_inline_blocks) | [CSS-live.ru](https://css-live.ru/articles-css/udivitelnyj-i-neizvestnyj-inline-block.html), [YouTube Алексей Пауков](https://www.youtube.com/watch?v=krsV53STWkE) |
| [БЭМ](#answer_bem) | - |
| [CSS контекст наложения](#answer_stacking_context) | - |
| [Babel](#answer_babel) | - |
| [Source map](#answer_sourse_map) | - |

<details>
  <summary markdown="span" name="answer_css_specificity"> CSS специфичность </summary>
  
  <h3 name="answer_css_specificity"> CSS специфичность </h3>
  
  Специфичность представляет собой вес (Важность :suspect:), придаваемый контректному правилу CSS.
  Вес правила определяется количеством каждого из типов селекторов.
  
  ### Типы селекторов по возрастанию специфичности
  
  0. Теговые селекторы (div, h1, h2) и псевдоэлементы (::after ::before)
  1. Классовые селекторы (.example), селекторы атрибутов ([type="checkbox"]) и псевдоклассы
  2. Индентификаторы (#example)
  
  Универсальный селектор (`*`), комбинаторы (`+`, `>`, `~`, '` `') и `:not()` не влияют на специфичность.<br>
  (Селекторы внутри `:not()` влияют)
  
  Стили объявленные внитри атрибута `style` имеют наивысшую специфичность<br>
  ```html
  <span style="red"> Я важный как х*й бумажный </span>
  ```
  
  ### Исключение `!important`
  
  Имеет наивысший приоритет
  
  #### Практика:
  
  + Всегда пытаться использовать специфичность, а `!important` использовать только в крайних случаях
  + Использовать `!important` только в страничных стилях которые переопределяют общие стили или стили библиотек (Bootstrap)
  + Не использовать `!important`, если пишешь плагин
  + Не использовать `!important` в общих стилях браузера
  
  ### Примеры
  
  ```html
<div id="test">
	<span>Text</span>
</div>
  ```
  ```css
div#test span { color: green }
div span { color: blue }
span { color: red }
  ```
  <img src="https://github.com/cclarice/kata-notepad/blob/main/assets/css-specificity-example.png">
  
  В данном примере текст зелёный так как `div#test span` имеет наивысшую специфичность, не смотря на их порядок
</details>
<details>
  <summary name="answer_inline_blocks"> Inline блоки </summary>
  Учитываются символы пробелов и табуляции
  Ведёт себя как inline (текстовый поток) и распологается по его правилам
</details>
<details>
  <summary name="answer_bem"> БЭМ </summary>
	
## БЭМ
  Это методология, правила вёрстки
### [Блок](#bem_block) [Элемент](#bem_element) [Модификатор](#bem_modificator)
### `block__element_modificator`

<h3 name="bem_block">Блок</h3>

&nbsp;&nbsp;&nbsp;&nbsp;Это функционально независимый компонент страницы, <br>
который может быть использован множество раз. <br>
&nbsp;&nbsp;&nbsp;&nbsp;Название класса блока должно отвечать <br>
на вопрос 'Что это?', а не как выглядит. <br>
&nbsp;&nbsp;&nbsp;&nbsp;Не стоит задавать блоку внешнюю геометрию (`margin` или `padding`), <br>
это позволяет перемещать и использовать блоки повторно <br>
никак не влияя на окружение. <br>
&nbsp;&nbsp;&nbsp;&nbsp;Блоки можно вкладывать в друг друга, <br>
Допустима любая вложеность блоков. <br>
&nbsp;&nbsp;&nbsp;&nbsp;Пример:
```html
<!-- Вложенность блоков -->

<!-- Блок `about` -->
<div class="about">
	<!-- Вложенный блок `title` -->
	<div class="title"></div>
	<!-- Вложенный бдлк `subtitle` -->
	<div class="subtitle"></div>
</div>
```

<h3 name="bem_element">Элемент</h3>
&nbsp;&nbsp;&nbsp;&nbsp;Это неотъемлемая составная часть блока, <br>
которая не может использоваться в отрыве от него. <br>
&nbsp;&nbsp;&nbsp;&nbsp;Имя элемента отвечает на вопрос `Что это?`<br>
&nbsp;&nbsp;&nbsp;&nbsp;Имя элемента наследует имя блока таким образом: <br>
`block__element`<br>
&nbsp;&nbsp;&nbsp;&nbsp;Элемент всегда должен быть частью блок и не должен <br>
использоваться вне блока <br>
&nbsp;&nbsp;&nbsp;&nbsp;Элемент это не обязательный компонент блока

Примеры:

1. Пример. Элемента в блоке навигации
```html
<nav class="menu">
	<a class="menu__link">Первый элемент меню</a>
	<a class="menu__link">Второй элемент меню</a>
	<a class="menu__link">Третий элемент меню</a>
</nav>
```
2. Пример. Элементы можно вкладывать друг в друга, <br>
Допустима любая вложенность элементов в элементы, <br>
элемент это всегда часть блока, а не другого элемента

```html
<!-- Блок `row` -->
<div class="row">
	<!-- Элемент `column` -->
	<div class="row__column">
		<!-- Элемент `item` -->
		<div class="row__item"></div>
	</div>
</div>
```

**ОШИБКОЙ** является подобная запись:
~~row__column__item~~

   

<h3 name="bem_modificator">Модификатор</h3>
&nbsp;&nbsp;&nbsp;&nbsp;Применяется для определения или уточнения <br>
внешнего вида, состояния или поведения блока или элемента <br>
&nbsp;&nbsp;&nbsp;&nbsp;Имя должно отвечать на вопрос `какой?`, <br>`как выглядит?`, `Как себя ведёт?` либо его `состояние`
&nbsp;&nbsp;&nbsp;&nbsp;Имя дополняет блок или элемент таким образом: <br>
`block_modificator`<br>
`block__element_modificator`<br>

Пример:

```html
<nav class="menu">
	<a class="menu__item menu__item_active">HOME</a>
	<a class="menu__item">ABOUT</a>
	<a class="menu__item">CONTACT</a>
</nav>
```

<h3> Миксы </h3>

Приём позволяющий использовать и блоки и элементы в одном объекте

Пример: 
```html
<!-- Блок `about` -->
<div class="about">
  <!-- Элемент `title` -->
  <div class="about__title title"></div>
  <!-- Элемент `subtitle` -->
  <div class="about__subtitle subtitle"></div>
</div>
```
</details>
<details>
  <summary name="answer_stacking_context"> CSS контекст наложения </summary>
  Ответ
</details>
<details>
  <summary name="answer_babel"> Babel </summary>
  Ответ
</details>
<details>
  <summary name="answer_sourse_map"> Source map </summary>
  Ответ
</details>
