# Список питань з JavaScript для blended занять

Відповіді знаходяться в згорнутій секції нижче питань. Просто натисни на відповідь, щоб розгорнути. Успіхів! :heart:

#### 1. Що буде в консолі?

```javascript
function sayHi() {
  console.log(name);
  console.log(age);
  let name = 'Lydia';
  let age = 21;
}

sayHi();
```

- A: `Lydia` та `undefined`
- B: `Lydia` та `ReferenceError`
- C: `ReferenceError` та `21`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: D

Всередині функції ми спершу визначаємо змінну `name` за допомогою ключового слова `let`. Це означає, що ми ще не визначили значення `name`, коли намагаємося вивести її в консоль, тому в консолі буде `ReferenceError`. Коли ми намагаємося звернутися до змінних до того моменту як вони визначені, JavaScript видає `ReferenceError`.

</p>
</details>

---

#### 2. Що буде в консолі?

```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```

- A: `0 1 2`
- B: `3 3 3`
- C: `0 1 2`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: C

Через черги подій в JavaScript, функція `setTimeout` викликається _після того_ як цикл буде завершено. Так як змінна `i` визначена за допомогою `let`. Такі змінні (а також `const`) мають блокову область видимості (блок це що завгодно між `{}`). З кожною ітерацією `i` матиме нове значення, і кожне значення буде замкнуто у своїй області видимості всередині циклу.

</p>
</details>

---

#### 3. Що буде в консолі?

```javascript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius,
};

shape.diameter();
shape.perimeter();
```

- A: `20` та `62.83185307179586`
- B: `20` та `NaN`
- C: `20` та `63`
- D: `NaN` та `63`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: B

Зауваж, що `diameter` це звичайна функція, в той час як `perimeter` це стрілкова функція.

У стрілкових функцій значення `this` вказує на навколишню область видимості, на відміну від звичайних функцій! Це означає, що при виклику `perimeter` значення `this` у цій функції вказує не на об'єкт `shape`, а на зовнішню область видимості (наприклад, window).

У цього об'єкта немає ключа `radius`, тому повертається `undefined`.

</p>
</details>

---

#### 4. Що буде в консолі?

```javascript
+true;
!'Lydia';
```

- A: `1` та `false`
- B: `false` та `NaN`
- C: `false` та `false`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

Унарний плюс призводить операнд до числа. `true` це `1`, а `false` це `0`.

Строка `'Lydia'` це "справжнє" значення. Ми запитуємо "справжнє значення є помилковим"? Відповідь: `false`.

</p>
</details>

---

#### 5. Що з цього не є коректним?

```javascript
const bird = {
  size: 'small',
};

const mouse = {
  name: 'Mickey',
  small: true,
};
```

- A: `mouse.bird.size` не є коректно
- B: `mouse[bird.size]` не є коректно
- C: `mouse[bird["size"]]` не є коректно
- D: Всі варіанти коректні

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

В JavaScript все ключі об'єкта є рядками (крім `Symbol`). І хоча ми не _набираємо_ їх як рядки, вони завжди перетворюються до рядків під капотом.

JavaScript інтерпретує (або розпаковує) оператори. При використанні квадратних дужок JS зауважує `[` і продовжує поки не зустріне `]`. Тільки після цього він вирахує то, що знаходиться всередині дужок.

`mouse[bird.size]`: Спершу визначається `bird.size`, що дорівнює `"small"`. `mouse["small"]` повертає `true`.

Але із записом через крапку так не відбувається. У `mouse` немає ключа `bird`. Таким чином, `mouse.bird` дорівнює `undefined`. Потім ми запитуємо ключ `size`, використовуючи крапкову нотацію: `mouse.bird.size`. Так як `mouse.bird` це `undefined`, ми запитуємо `undefined.size`. Це не є дійсним, тому ми отримуємо помилку типу: `Can not read property "size" of undefined`.

</p>
</details>

---

#### 6. Що буде в консолі?

```javascript
let c = { greeting: 'Hey!' };
let d;

d = c;
c.greeting = 'Hello';
console.log(d.greeting);
```

- A: `Hello`
- B: `Hey`
- C: `undefined`
- D: `ReferenceError`
- E: `TypeError`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

В JavaScript всі об'єкти є _посилальними_ типами даних.

Спершу змінна `c` вказує на об'єкт. Потім ми вказуємо змінної `d` посилатися на той самий об'єкт, що і `c`.

<img src="https://i.imgur.com/ko5k0fs.png" width="200">

Коли ти змінюєш один об'єкт, то змінюються значення всіх посилань, що вказують на цей об'єкт.

</p>
</details>

---

#### 7. Що буде в консолі?

```javascript
let a = 3;
let b = new Number(3);
let c = 3;

console.log(a == b);
console.log(a === b);
console.log(b === c);
```

- A: `true` `false` `true`
- B: `false` `false` `true`
- C: `true` `false` `false`
- D: `false` `true` `true`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: C

`new Number()` це вбудований конструктор функції. І хоча він виглядає як число, це не справжнє число: у нього є ряд додаткових фіч і це об'єкт.

Оператор `==` призводить типи даних до якогось одного і перевіряє рівність _значень_. Обидва значення рівні `3`, тому повертається `true`.

При використанні оператора `===` значення і тип повинні бути однаковими. Але в нашому випадку це не так: `new Number()` це не число, це **об'єкт**. Тому обидва повертають `false`.

</p>
</details>

---

#### 8. Яким буде результат?

```javascript
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor;
    return this.newColor;
  }

  constructor({ newColor = 'green' } = {}) {
    this.newColor = newColor;
  }
}

const freddie = new Chameleon({ newColor: 'purple' });
freddie.colorChange('orange');
```

- A: `orange`
- B: `purple`
- C: `green`
- D: `TypeError`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: D

Функція `colorChange` є статичною. Статичні методи не мають доступу до екземплярів класу. Так як `freddie` це екземпляр, то статичний метод там не доступний. Тому результатом є помилка `TypeError`.

</p>
</details>

---

#### 9. Що станеться?

```javascript
function bark() {
  console.log('Woof!');
}

bark.animal = 'dog';
```

- A: Нічого, все ок.
- B: `SyntaxError`. Не можна додавати властивості функцій таким способом.
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

В JavaScript це можливо, тому що функції це об'єкти! (Все є об'єктами крім примітивів).

Функція - це спеціальний тип об'єкта, який можна викликати. Крім того, функція - це об'єкт з властивостями. Властивість такого об'єкта не можна викликати, так як воно не є функцією.

</p>
</details>

---

#### 10. Що буде в консолі?

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person('Lydia', 'Hallie');
Person.getFullName = function () {
  return `${this.firstName} ${this.lastName}`;
};

console.log(member.getFullName());
```

- A: `TypeError`
- B: `SyntaxError`
- C: `Lydia Hallie`
- D: `undefined` `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

Не можна додавати властивості конструктору, як звичайному об'єкту. Якщо потрібно додати фічу до всіх об'єктів, то необхідно використовувати прототипи. В даному випадку,

```js
Person.prototype.getFullName = function () {
  return `${this.firstName} ${this.lastName}`;
};
```

зробить метод `member.getFullName()` чинним. У чому тут перевага? Припустимо, що ми додали цей метод до конструктора. Можливо, не кожному екземпляру `Person` потрібен цей метод. Це призведе до великих втрат пам'яті, тому що всі екземпляри будуть мати цю властивість. Навпаки, якщо ми додамо цей метод тільки до прототипу, у нас буде тільки одне місце в пам'яті, до якого зможуть звертатися всі екземпляри!

</p>
</details>

---

#### 11. Що буде в консолі?

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const lydia = new Person('Lydia', 'Hallie');
const sarah = Person('Sarah', 'Smith');

console.log(lydia);
console.log(sarah);
```

- A: `Person {firstName: "Lydia", lastName: "Hallie"}` та `undefined`
- B: `Person {firstName: "Lydia", lastName: "Hallie"}` та `Person {firstName: "Sarah", lastName: "Smith"}`
- C: `Person {firstName: "Lydia", lastName: "Hallie"}` та `{}`
- D:`Person {firstName: "Lydia", lastName: "Hallie"}` та `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

Для `sarah` ми не використали ключове слово `new`. Використання `new` призводить до створення нового об'єкта. Але без `new` він вказує на **глобальний об'єкт**!

Ми вказали, що `this.firstName` дорівнює `"Sarah"` і `this.lastName` дорівнює `"Smith"`. Насправді ми визначили `global.firstName = 'Sarah'` і `global.lastName = 'Smith'`. `sarah` залишилася `undefined`.

</p>
</details>

---

#### 12. Назвіть три фази поширення подій

- A: Мета (Target) > Захоплення (Capturing) > Спливання (Bubbling)
- B: Спливання (Bubbling) > Мета (Target) > Захоплення (Capturing)
- C: Мета (Target) > Спливання (Bubbling) > Захоплення (Capturing)
- D: Захоплення (Capturing) > Мета (Target) > Спливання (Bubbling)

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: D

Під час фази **захоплення** подія поширюється від батьківського елемента до елемента мети. Після досягнення **мети** починається фаза **спливання**.

<img src="https://i.imgur.com/N18oRgd.png" width="200">

</p>
</details>

---

#### 13. Всі об'єкти мають прототипи?

- A: Так
- B: Ні

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: B

Всі об'єкти мають прототипи, крім **базового об'єкта**. Базовий об'єкт має доступ до деяких методів і властивостей, таких як `.toString`. Саме тому ми можемо використовувати вбудовані методи JavaScript! Всі ці методи доступні в прототипі. Якщо JavaScript не може знайти метод безпосередньо у об'єкту, він продовжує пошук по ланцюжку прототипів поки не знайде.

</p>
</details>

---

#### 14. Результат коду?

```javascript
function sum(a, b) {
  return a + b;
}

sum(1, '2');
```

- A: `NaN`
- B: `TypeError`
- C: `"12"`
- D: `3`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: C

JavaScript це **динамічно типізована мова**: ми не визначаємо тип змінних. Змінні можуть автоматично бути перетворені з одного типу в інший без нашої участі, що називається _неявним приведенням типів_. **Приведення** це перетворення з одного типу в інший.

У цьому прикладі, JavaScript конвертувати число `1` в рядок, щоб операція всередині функції мала сенс і повернула значення. Під час складання числа (`1`) і рядки (`'2'`) число перетворюється до рядка. Ми можемо додавати рядки ось так: `"Hello" + "World"`. Таким чином, "`1"` + `"2"` повертає "`12"`.

</p>
</details>

---

#### 15. Що буде в консолі?

```javascript
function getPersonInfo(one, two, three) {
  console.log(one);
  console.log(two);
  console.log(three);
}

const person = 'Lydia';
const age = 21;

getPersonInfo`${person} is ${age} years old`;
```

- A: `"Lydia"` `21` `["", " is ", " years old"]`
- B: `["", " is ", " years old"]` `"Lydia"` `21`
- C: `"Lydia"` `["", " is ", " years old"]` `21`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: B

При використанні тегованих шаблонних літералів першим аргументом завжди буде масив строкових значень. Решта аргументів будуть значення мати переданих виразів!

</p>
</details>

---

#### 16. Що буде в консолі?

```javascript
function checkAge(data) {
  if (data === { age: 18 }) {
    console.log('You are an adult!');
  } else if (data == { age: 18 }) {
    console.log('You are still an adult.');
  } else {
    console.log(`Hmm.. You don't have an age I guess`);
  }
}

checkAge({ age: 18 });
```

- A: `You are an adult!`
- B: `You are still an adult.`
- C: `Hmm.. You don't have an age I guess`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: C

В операціях порівняння примітиви порівнюються за їх _значенням_, а об'єкти за _посиланнями_. JavaScript перевіряє, щоб об'єкти вказували на одну і ту ж область пам'яті.

Порівнювані об'єкти в нашому прикладі не такі: об'єкт, переданий як параметр, вказує на іншу область пам'яті, ніж об'єкти, що використовуються в порівнянні.

Тому `{age: 18} === {age: 18}` і `{age: 18} == {age: 18}` повертають `false`.

</p>
</details>

---

#### 17. Що буде в консолі?

```javascript
function getAge(...args) {
  console.log(typeof args);
}

getAge(21);
```

- A: `"number"`
- B: `"array"`
- C: `"object"`
- D: `"NaN"`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: C

Оператор поширення (`... args`) повертає масив з аргументами. Масив це об'єкт, тому `typeof args` повертає `"object"`.

</p>
</details>

---

#### 18. Що буде в консолі?

```javascript
function getAge() {
  'use strict';
  age = 21;
  console.log(age);
}

getAge();
```

- A: `21`
- B: `undefined`
- C: `ReferenceError`
- D: `TypeError`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: C

Використовуючи `"use strict"`, можна бути впевненим, що ми помилково не оголосимо глобальні змінні. Ми раніше ніде не оголошували змінну `age`, тому з використанням `"use strict"` виникне ReferenceError. Без використання `"use strict"` помилки не виникне, а змінна `age` додасться в глобальний об'єкт.

</p>
</details>

---

#### 19. Що буде в консолі?

```javascript
let num = 8;
const age = num;
num = 21;

console.log(age);
```

- A: `8`
- B: `10`
- C: `SyntaxError`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

`let num = 8`
Створюється змінна `num` і їй присвоюється значення `8`.

`const age = num;`
Створюється константа `age` і їй присвоюється поточне значення змінної `num`, тобто `8`.
При цьому значення `age` є копією значення `num`, а не посиланням на саму змінну `num`.

`num = 21;`
Значення змінної `num` змінюється на `21`. Це не впливає на `age`, оскільки значення `8` вже було скопійоване раніше.

У JavaScript примітивні типи даних (числа, рядки, булеві значення тощо) передаються за значенням, а не за посиланням.
Тому коли ми присвоюємо `const age = num`, значення `8` копіюється в `age`, і подальші зміни змінної `num` не впливають на значення `age`.

</p>
</details>

---

#### 20. Що буде в консолі?

```javascript
const obj = { a: 'one', b: 'two', a: 'three' };
console.log(obj);
```

- A: `{ a: "one", b: "two" }`
- B: `{ b: "two", a: "three" }`
- C: `{ a: "three", b: "two" }`
- D: `SyntaxError`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: C

Якщо є два ключі з однаковим ім'ям, то ключ буде перезаписаний. Його позиція збережеться, але значенням буде встановлено останнім.

</p>
</details>

---

#### 21. Глобальний контекст виконання створює дві речі: глобальний об'єкт і this

- A: Так
- B: Ні
- C: В залежності від ситуації

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

Базовий контекст виконання це глобальний контекст виконання: це те, що є де завгодно у твоєму коді.

</p>
</details>

---

#### 22. Що буде в консолі?

```javascript
for (let i = 1; i < 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
```

- A: `1` `2`
- B: `1` `2` `3`
- C: `1` `2` `4`
- D: `1` `3` `4`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: C

Оператор `continue` пропускає ітерацію, якщо умова повертає `true`.

</p>
</details>

---

#### 23. Що буде в консолі?

```javascript
const a = {};
const b = { key: 'b' };
const c = { key: 'c' };

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

- A: `123`
- B: `456`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: B

Ключі об'єкта автоматично конвертуються в рядки. Ми збираємося додати об'єкт в якості ключа до об'єкта `a` зі значенням `123`.

Проте, коли ми наводимо об'єкт до рядка, він стає `"[object Object]"`. Таким чином, ми говоримо, що `a["object Object"] = 123`. Потім ми робимо те ж саме. `c` це інший об'єкт, який ми неявно наводимо до рядка. Тому `a["object Object"] = 456`.

Потім, коли ми виводимо `a[b]`, ми маємо на увазі `a["object Object"]`. Ми тільки що встановили туди значення `456`, тому в результаті отримуємо `456`.

</p>
</details>

---

#### 24. Яким буде результат?

```javascript
const foo = () => console.log('First');
const bar = () => setTimeout(() => console.log('Second'));
const baz = () => console.log('Third');

bar();
foo();
baz();
```

- A: `First` `Second` `Third`
- B: `First` `Third` `Second`
- C: `Second` `First` `Third`
- D: `Second` `Third` `First`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: B

Ми викликаємо функцію `setTimeout` першою. Тим не менш, вона виводиться в консоль останньою.

Це відбувається через те, що в браузерах у нас є не тільки рантайм движок, але і `WebAPI`. `WebAPI` надає нам функцію `setTimeout` і багато інших можливостей. Наприклад, DOM.

Після того як _коллбек_ відправлений в `WebAPI`, функція `setTimeout` (але не коллбек!) виймається з стека.

<img src="https://i.imgur.com/X5wsHOg.png" width="200">

Тепер викликається `foo`, і `"First"` виводиться в консоль.

<img src="https://i.imgur.com/Pvc0dGq.png" width="200">

`foo` дістається з стека, і викликається `baz`. `"Third"` виводиться в консоль.

<img src="https://i.imgur.com/WhA2bCP.png" width="200">

`WebAPI` не може додавати вміст в стек коли захоче. Замість цього він відправляє коллбек-функцію в так звану _чергу_.

<img src="https://i.imgur.com/NSnDZmU.png" width="200">

Тут на сцену виходить цикл подій (event loop). **Event loop** перевіряє стек і черга завдань. Якщо стек порожній, то він бере перший елемент з черги і відправляє його в стек.

<img src="https://i.imgur.com/uyiScAI.png" width="200">

Викликається `bar`, в консоль виводиться `"Second"` і ця функція дістається з стека.

</p>
</details>

---

#### 25. Що буде в `event.target` після кліка на кнопку?

```html
<div onclick="console.log('first div')">
  <div onclick="console.log('second div')">
    <button onclick="console.log('button')">Click!</button>
  </div>
</div>
```

- A: Зовнішній `div`
- B: Внутрішній `div`
- C: `button`
- D: Масив з усіма вкладеними елементами

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: C

Метою події є **найглибший** вкладений елемент. Зупинити поширення подій можна за допомогою `event.stopPropagation`

</p>
</details>

---

#### 26. Що буде в консолі після кліка по параграфу?

```html
<div onclick="console.log('div')">
  <p onclick="console.log('p')">Click here!</p>
</div>
```

- A: `p` `div`
- B: `div` `p`
- C: `p`
- D: `div`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

Після кліка по `p` буде виведено `p` та `div`. У циклі життя події є три фази: **захоплення**, **мета** і **спливання**. За замовчуванням обробники подій виконуються на фазі спливання (якщо не встановлено параметр `useCapture` в `true`). Спливання йде з найглибшого елемента вгору.

</p>
</details>

---

#### 27. Що буде в консолі?

```javascript
const person = { name: 'Lydia' };

function sayHi(age) {
  console.log(`${this.name} is ${age}`);
}

sayHi.call(person, 21);
sayHi.bind(person, 21);
```

- A: `undefined is 21` `Lydia is 21`
- B: `function` `function`
- C: `Lydia is 21` `Lydia is 21`
- D: `Lydia is 21` `function`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: D

В обох випадках ми передаємо об'єкт, на який буде вказувати `this`. Але `.call` виконується _відразу ж_!

`.bind` повертає _копію_ функції, але з прив'язаним контекстом. Вона не виконується негайно.

</p>
</details>

---

#### 28. Яким буде результат?

```javascript
function sayHi() {
  return (() => 0)();
}

typeof sayHi();
```

- A: `"object"`
- B: `"number"`
- C: `"function"`
- D: `"undefined"`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: B

Функція `sayHi` повертає значення, що повертається з _негайно викликаного функціонального виразу_ (IIFE). Результатом є `0` типу `"number"`.

Для інформації: в JS 7 вбудованих типів: `null`, `undefined`, `boolean`, `number`, `string`, `object`, `symbol`, та `bigint`. `"Function"` не є окремим типом, тому що функції є об'єктами типу `"object"`.

</p>
</details>

---

#### 29. Які з цих значень є "помилковими" (приводяться до false)?

```javascript
0;
new Number(0);
('');
(' ');
new Boolean(false);
undefined;
```

- A: `0`, `''`, `undefined`
- B: `0`, `new Number(0)`, `''`, `new Boolean(false)`, `undefined`
- C: `0`, `''`, `new Boolean(false)`, `undefined`
- D: Всі значення.

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

Є тільки шість "помилкових" значень:

- `undefined`
- `null`
- `NaN`
- `0`
- `''` (порожній рядок)
- `false`

Конструктори функцій, такі як new `Number` та `new Boolean` є "істинними".

</p>
</details>

---

#### 30. Що буде в консолі?

```javascript
console.log(typeof typeof 1);
```

- A: `"number"`
- B: `"string"`
- C: `"object"`
- D: `"undefined"`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: B

`typeof 1` повертає `"number"`.
`typeof "number"` повертає `"string"`

</p>
</details>

---

#### 31. Що буде в консолі?

```javascript
const numbers = [1, 2, 3];
numbers[10] = 11;
console.log(numbers);
```

- A: `[1, 2, 3, 7 x null, 11]`
- B: `[1, 2, 3, 11]`
- C: `[1, 2, 3, 7 x empty, 11]`
- D: `SyntaxError`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: C

Коли в масив додається значення, яке виходить за межі довжини масиву, JavaScript створює так звані "порожні клітинки". Насправді вони мають значення `undefined`, але в консолі виводяться так:

`[1, 2, 3, 7 x empty, 11]`

в залежності від місця використання (може відрізнятися для браузерів, Node, і т.д.).

</p>
</details>

---

#### 32. Все в JavaScript це...

- A: примітив або об'єкт
- B: функція або об'єкт
- C: питання з підступом! тільки об'єкти
- D: число або об'єкт

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

В JavaScript є тільки примітиви й об'єкти.

Типи примітивів: `boolean`, `null`, `undefined`, `bigint`, `number`, `string`, та `symbol`.

Відмінністю примітиву від об'єкта є те, що примітиви не мають властивостей або методів. Проте, `'foo'.toUpperCase()` перетворюється в `'FOO'` та не викликає `TypeError`. Це відбувається тому, що при спробі отримання властивості або методу у примітиву (наприклад, рядки), JavaScript неявно оберне примітив об'єктом, використовуючи один з класів-обгорток (наприклад, `String`), а потім відразу ж знищить обгортку після обчислення виразу. Всі примітиви крім `null` та `undefined` поводяться таким чином.

</p>
</details>

---

#### 33. Що буде в консолі?

```javascript
[
  [0, 1],
  [2, 3],
].reduce(
  (acc, cur) => {
    return acc.concat(cur);
  },
  [1, 2]
);
```

- A: `[0, 1, 2, 3, 1, 2]`
- B: `[6, 1, 2]`
- C: `[1, 2, 0, 1, 2, 3]`
- D: `[1, 2, 6]`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: C

`[1, 2]` - початкове значення, з яким ініціалізується змінна `acc`. Після першого проходу `acc` дорівнюватиме `[1,2]`, а `cur` буде `[0,1]`. Після конкатенації результат буде `[1, 2, 0, 1]`.

Потім `acc` дорівнює `[1, 2, 0, 1]`, а cur `[2, 3]`. Після злиття отримаємо `[1, 2, 0, 1, 2, 3]`.

</p>
</details>

---

#### 34. Що буде в консолі?

```javascript
!!null;
!!'';
!!1;
```

- A: `false` `true` `false`
- B: `false` `false` `true`
- C: `false` `true` `true`
- D: `true` `true` `false`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: B

`null` "НЕправдивий". `!null` повертає `true`. `!true` повертає `false`.

`""` "НЕправдивий". `!""` повертає `true`. `!true` повертає `false`.

`1` "правдивий". `!1` повертає `false`. `!false` повертає `true`.

</p>
</details>

---

#### 35. Що повертає метод `setInterval`?

```javascript
setInterval(() => console.log('Hi'), 1000);
```

- A: унікальний id
- B: вказану кількість мілісекунд
- C: передану функцію
- D: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

Цей метод повертає унікальний id, який може бути використаний для очищення інтервалу за допомогою функції `clearInterval()`.

</p>
</details>

---

#### 36. Що повернеться?

```javascript
[...'Lydia'];
```

- A: `["L", "y", "d", "i", "a"]`
- B: `["Lydia"]`
- C: `[[], "Lydia"]`
- D: `[["L", "y", "d", "i", "a"]]`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: A

Рядок є ітерабельною сутністю. Оператор поширення перетворює кожен символ в окремий елемент.

</p>
</details>

---

#### 37. Що повернеться?

```javascript
const firstPromise = new Promise((res, rej) => {
  setTimeout(res, 500, 'one');
});

const secondPromise = new Promise((res, rej) => {
  setTimeout(res, 100, 'two');
});

Promise.race([firstPromise, secondPromise]).then((res) => console.log(res));
```

- A: `"one"`
- B: `"two"`
- C: `"two" "one"`
- D: `"one" "two"`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: B

Коли ми передаємо кілька промісів методу `Promise.race`, він вирішує/відхиляє _перший_ проміс, яки вирішився/відхилився. Методу `setTimeout` ми передаємо таймер: 500 мс для першого промісу (`firstPromise`) та 100 мс для другого промісу (`secondPromise`). Це означає, що `secondPromise` вирішиться першим зі значенням `'two'`. `res` тепер містить значення `'two'`, яке буде зображено у консолі.

</p>
</details>

---

#### 38. Що буде на виході?

```javascript
let person = { name: 'Lydia' };
const members = [person];
person = null;

console.log(members);
```

- A: `null`
- B: `[null]`
- C: `[{}]`
- D: `[{ name: "Lydia" }]`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: D

Спочатку ми оголошуємо змінну `person` що містить об'єкта, який має властивість `name`.

<img src="https://i.imgur.com/TML1MbS.png" width="200">

Потім ми оголошуємо змінну `members`. Ми встановлюємо перший елемент масиву рівним значенню змінної `person`. Об'єкти взаємодіють за допомогою _посилання_, коли їх встановлюють рівними один одному. Коли ви призначаєте посилання з однієї змінної на іншу, ви робите _копію_ цього посилання. (зверніть увагу, що вони не мають _однакового_ посилання!)

<img src="https://i.imgur.com/FSG5K3F.png" width="300">

Далі ми встановлюємо змінну `person` рівною `null`.

<img src="https://i.imgur.com/sYjcsMT.png" width="300">

Ми лише змінюємо значення змінної `person`, а не перший елемент у масиві, оскільки цей елемент має інше (скопійоване) посилання на об’єкт.Перший елемент у `members` все ще містить своє посилання на вихідний об’єкт. Коли ми виводимо у консоль масив `members`, перший елемент усе ще містить значення об'єкта, який і показується у консолі.

</p>
</details>

---

#### 39. В якому порядку будуть виведені console.log?

```javascript
const ParentComponent = () => {
  console.log('A');

  useEffect(() => {
    console.log('B');
  }, []);

  return <ChildComponent />;
};

const ChildComponent = () => {
  console.log('C');

  useEffect(() => {
    console.log('D');
  }, []);

  return <p>Hello world</p>;
};
```

- A: `A > D > B > C`
- B: `C > A > D > B`
- C: `A > D > C > B`
- D: `A > C > D > B`

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: D

`A` — Лог з `ParentComponent`, оскільки тіло компонента виконується під час його рендеру.\
`C` — Лог з `ChildComponent`, оскільки `ChildComponent` рендериться після `ParentComponent`.\
`D` — Лог з `useEffect` у `ChildComponent`. `useEffect` виконується після рендеру `ChildComponent`.\
`B` — Лог з `useEffect` у `ParentComponent`. `useEffect` виконується після рендеру компонента.

</p>
</details>

---

#### 40. Напиши код щоб розвернути рядок задом наперед не використовуючи метод reverse?

```javascript
function reverseString(str) {
  // ...
}
const input = 'Hello, world!';
const output = reverseString(input);
console.log(output); // "!dlrow ,olleH"
```

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь:

```javascript
function reverseString(str) {
  let reversed = '';
  const length = str.length;

  for (let i = 0; i < Math.ceil(length / 2); i++) {
    // Додаємо символ з кінця та з початку (індекс i та length - i - 1)
    if (i !== length - i - 1) {
      reversed = str[i] + reversed + str[length - i - 1];
    } else {
      // Для середнього символу (в разі непарної довжини рядка)
      reversed = str[i] + reversed;
    }
  }

  return reversed;
}
const input = 'Hello, world!';
const output = reverseString(input);
console.log(output); // "!dlrow ,olleH"
```

Паралельна обробка символів:
Ітеруємося лише до середини рядка.
Додаємо символ з початку `(str[i])` і з кінця `(str[length - i - 1])` у зворотному порядку.

Скорочення ітерацій:
Замість проходу через весь рядок, цикл виконується лише половину кількості разів.
Обробка середнього символу:

У випадку непарної довжини рядка середній символ додається лише один раз.

</p>
</details>

---

#### 41. Чому ми можемо використовувати метод toLowerCase() для змінної name, якщо вона є рядком?

```javascript
const name = 'Mango';

name.toLowerCase();
```

`A` Метод `toLowerCase` автоматично додається до всіх змінних у `JavaScript`.
`B` `toLowerCase` — це вбудований метод, доступний для всіх рядкових значень у `JavaScript`, оскільки він є частиною прототипу об'єкта `String`.
`C` Метод `toLowerCase` був оголошений вручну для змінної name у коді.
`D` Метод `toLowerCase` працює для всіх типів даних у `JavaScript`, не лише для рядків.

<details><summary><b>Відповідь</b></summary>
<p>

##### Відповідь: B

`toLowerCase` — це вбудований метод, доступний для всіх рядкових значень у JavaScript, оскільки він є частиною прототипу об'єкта `String`.

</p>
</details>
