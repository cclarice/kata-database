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
| [Inline блоки](#answer_inline_blocks) | [CSS-live.ru](https://css-live.ru/articles-css/udivitelnyj-i-neizvestnyj-inline-block.html) |
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
  Ответ
</details>
<details>
  <summary name="answer_bem"> БЭМ </summary>
  Ответ
</details>
<details>
  <summary name="answer_stacking_context"> [CSS контекст наложения </summary>
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
