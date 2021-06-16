# Best_PracticesJS

## Переменные

### 1. Избегайте глобальных переменных

Минимизируйте использование глобальных переменных.
Это включает в себя все типы данных, объекты и функции.
Глобальные переменные и функции могут быть перезаписаны другими скриптами.
Вместо этого используйте локальные переменные и научитесь использовать замыкания.

### 2. Всегда объявляйте локальные переменные

Как следствие, мы должны всегда объявлять локальные переменные и постоянные также с помощью var, let или const. 
В противном случае переменная будет объявлена как глобальная и как свойство объекта window, чего мы определенно не хотим. 

Например, никогда не стоит писать:
```
x = 1;
```

Следует писать так:
```
let x = 1;
```

К счастью, JavaScript strict mode (строгий режим) не позволяет необъявленные переменные, поэтому случайно создать глобальные переменные нельзя.

В модулях JavaScript strict mode тоже доступен по умолчанию, поэтому и в них невозможно случайно создать глобальные переменные. 

### 3. Имена переменных и функций

Названия функций и переменных могут содержать латинские буквы, цифры и знак $, но имена должны начинаться с латинской буквы. 
В имени переменной или функции должно отображаться её содержание. 
Если название переменной или функции состоит из нескольких слов, то каждое последующее слово пишется с заглавной буквы( js чувствителен к регистру).
  
Как не стоит называть переменные или функции: 
    
 ``` 
    let a = Sergey;
    const 5m = 25 ;
    function abc();
    function startplay();
 ```
 
Хорошие примеры: 
   
 ``` 
   let name = Sergey;
   const number = 25;
   function startPlay();
   function read45Page();
 ```

### 4. Переменные и константы должны быть наверху 

Объявление переменных и вверху файла делает код чище. Также это помешает случайно ссылаться на переменные, объявленные с let или const до того, как они будут определены. 

Если strict mode выключен, мы также избегаем создания глобальных переменных и случайного повторного объявления. 
Большинство текстовых редакторов отлавливает повторные объявления, но вероятность пропустить их остается. 

Можно объявить несколько переменных в одной строке, разделив имена запятыми. 

Например, мы можем написать:
```
let x, y;
x = 1;
y = 1;
console.log(x, y);
```
И тогда мы из console.log. получим:
```
1 1
```

То же самое можно сделать с помощью цикла: 
```
let i;

for (i = 0; i < 10; i++) {
  console.log(i);
}
```

### 5. Инициализируйте переменные при их объявлении

Инициализировать переменные и константы с объявленными значениями весьма хорошая идея. Это предотвращает ошибки неопределенных значений. 
Также удобно объявлять переменные или константы и задавать их начальные значения одной строкой. 

В противном случае у нас будут отдельные строки для объявления и для значения. 

Например, мы можем написать:
```
let x = 1,
  y = 1;
```  
Чтобы объявить и x, и y. 

Это существенно короче, чем: 
```
let x;
let y;
x = 1;
y = 1;
```
Мы можем объявлять и инициализировать несколько переменных, разделив каждое объявление и назначение запятыми. 

### 6. Объекты

Никогда не объявляйте числовые (number), строковые (string) или логические (boolean) объекты
Всегда обрабатывайте числа, строки или логические значения как примитивные значения. Но не как объекты.

Объявление этих типов как объектов замедляет скорость выполнения и вызывает неприятные побочные эффекты: 

```
var x = "John";             
var y = new String("John");
(x === y) // является false, потому что x является строкой и y является объектом.
```

Или еще хуже:
```
var x = new String("John");             
var y = new String("John");
(x == y) // является false, потому что вы не можете сравнивать объекты.
```

### 7. Автоматическое преобразование типов

Остерегайтесь автоматических преобразований типов
Помните, что числа могут быть случайно преобразованы в строки или `NaN` (Not a Number / Не число).

JavaScript слабо типизирован. Переменная может содержать разные типы данных, а переменная может изменять свой тип данных:
```
var x = "Hello";     // по типу x является строкой
x = 5;               // изменение типа x на число
```

При выполнении математических операций JavaScript может преобразовывать числа в строки:
```
var x = 5 + 7;       // x.valueOf() является 12,  тип x является числом
var x = 5 + "7";     // x.valueOf() является 57,  тип x является строкой
var x = "5" + 7;     // x.valueOf() является 57,  тип x является строкой
var x = 5 - 7;       // x.valueOf() является -2,  тип x является числом
var x = 5 - "7";     // x.valueOf() является -2,  тип x является числом
var x = "5" - 7;     // x.valueOf() является -2,  тип x является числом
var x = 5 - "x";     // x.valueOf() является NaN, тип x является числом
```

Вычитание строки из строки не генерирует ошибку, но возвращает `NaN` (Not a Number):
```
"Hello" - "Dolly"    // возвращает NaN
```

### 8. Параметры по умолчанию

Использование параметров по умолчанию
Если функция вызывается с отсутствующим аргументом, значение отсутствующего аргумента устанавливается в `undefined` (не определено).

Неопределенные значения могут нарушить ваш код. Это хорошая привычка назначать значения по умолчанию для аргументов:
```
function myFunction(x, y) {
  if (y === undefined) {
    y = 0;
  }
}
```

## Производительность

### 9. Ограничение доступа к переменным и свойствам

Задача состоит в том, чтобы сократить время доступа к переменным и свойствам объектов в приложениях.

Причина заключается в том, что при каждом обращении процессору необходимо получить доступ к элементу в памяти, чтобы вычислить его результаты. 
Следовательно, это действие нужно выполнять как можно реже.

Например, при наличии цикла не нужно писать следующее:
```
for (let i = 0; i < arr.length; i++) {}
```

Лучше использовать данный вариант:
```
let length = arr.length;
for (let i = 0; i < length; i++) {}
```
Таким образом, на arr.length ссылаются один раз за цикл, а не обращаются к нему на каждой итерации.

### 10. Не объявляйте ненужные переменные

При каждом объявлении переменных, браузер должен выделить пространство памяти для них. 
Следовательно, чтобы уменьшить использование памяти, необходимо сократить количество объявления переменных.

Для примера возьмем следующий HTML-код:
```
<div id='foo'>
  <p>

  </p>
</div>
```

Чтобы установить текстовое содержимое элемента p, не нужно писать ничего вроде:
```
const foo = document.querySelector('#foo');
const p = foo.querySelector('p');
p.textContent = 'foo';
```
поскольку у нас есть 2 переменные. Это означает, что компьютер должен хранить значения еще для 2 переменных JavaScript.

Вместо этого можно сократить объявления переменных с помощью:
```
document.querySelector('#foo p').textContent = 'foo';
```
Используйте метод querySelector, а также связанный метод querySelectorAll, для выбора элементов, поскольку они оба применяют CSS-селекторы для выбора любого узла элемента HTML.

