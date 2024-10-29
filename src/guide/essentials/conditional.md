# Умовний рендеринг {#conditional-rendering}

<div class="options-api">
  <VueSchoolLink href="https://vueschool.io/lessons/conditional-rendering-in-vue-3" title="Безкоштовний урок по умовному рендеринг у Vue.js"/>
</div>

<div class="composition-api">
  <VueSchoolLink href="https://vueschool.io/lessons/vue-fundamentals-capi-conditionals-in-vue" title="Безкоштовний урок по умовному рендеринг у Vue.js"/>
</div>

<script setup>
import { ref } from 'vue'
const awesome = ref(true)
</script>

## `v-if` {#v-if}

Директива `v-if` використовується для умовного рендерингу блоку. Блок буде згенеровано лише якщо вираз у директиві повертає правдиве значення.

```vue-html
<h1 v-if="awesome">Vue — це круто!</h1>
```

## `v-else` {#v-else}

Ви можете використовувати директиву `v-else` для вказування "блоку інакше" для `v-if`:

```vue-html
<button @click="awesome = !awesome">Перемкнути</button>

<h1 v-if="awesome">Vue — це круто!</h1>
<h1 v-else>Ой, ні 😢</h1>
```

<div class="demo">
  <button @click="awesome = !awesome">Перемкнути</button>
  <h1 v-if="awesome">Vue — це круто!</h1>
  <h1 v-else>Ой, ні 😢</h1>
</div>

<div class="composition-api">

[Спробуйте в пісочниці](https://play.vuejs.org/#eNpFjkFKAzEUhq/ymk0V1KFbSQe9hKts6vCGDs4kIXmpi1IYFDyBiCsL3mFAi/YML1foCXqEpu3Q7t4P3/fx5uLe2ptZQHErpC9cZQk8UrC50lVjjSOYg8MSFlA608AwoUOllS6M9gSTZ/SmQRjvmQtyAS+VltkxlBJpEDa2nhCmBSAfA5HRcFfUVfE0VuIcGPSnEjkvuYstd/zHK/6Pr/GFf2R2VA9RRXI6gtl1VZ4TyXsICJv2HeIbd8Cr2B7U9UBm09He6y2sPeb8xb9XkOofsF1+fveIzE7visUOYEdzwQ==)

</div>
<div class="options-api">

[Спробуйте в пісочниці](https://play.vuejs.org/#eNpFjlFqwkAQhq8y7lMLbYOvsob2En3al20cMTQmy2bWFkQILfQEpfSpQu8QUFHPMHsFT+AR3JigyzLMz8z3MXPxZMzDzKEYCFkmNjUUqxzfTWEJRjjWLiOYqxxgpEnf3La9IovkbN4kRRCefsOymOIAyDpsVxbNLJTwZXRRh0A4NZkmDAlAvjiiIofHJEuT16ESnQmG0OtaJWJecu0rrnnLG975T//BKxm16FmqSE76MLtPx1dF4J4dwqH6Bv/FNfDGV2d035PRpN9wHYVZiTH/8foOgv0Hjsvf/25FRpdzxeIEV4B52A==)

</div>

Елемент з `v-else` повинен йти безпосередньо за елементом з `v-if` або елементом з `v-else-if` — в іншому випадку їх не буде розпізнано.

## `v-else-if` {#v-else-if}

`v-else-if`, як і підказує його назва, слугує в якості "блоку інакше якщо" для `v-if`. Може бути також і ланцюжок таких елементів:

```vue-html
<div v-if="type === 'А'">
  А
</div>
<div v-else-if="type === 'Б'">
  Б
</div>
<div v-else-if="type === 'В'">
  В
</div>
<div v-else>
  Не А/Б/В
</div>
```

Подібно до `v-else`, елемент з `v-else-if` повинен йти безпосередньо за `v-if` або за елементами з `v-else-if`.

## `v-if` в `<template>` {#v-if-on-template}

Оскільки `v-if` є директивою, вона має бути додана до одиничного елементу. Але що робити у випадку, коли ми хочемо перемикати більше, ніж один елемент? У такому разі ми можемо використовувати `v-if` в елементі `<template>`, який слугує невидимою обгорткою. Фінальний результат рендеру не міститиме `<template>`.

```vue-html
<template v-if="ok">
  <h1>Заголовок</h1>
  <p>Параграф 1</p>
  <p>Параграф 2</p>
</template>
```

Директиви `v-else` та `v-else-if` також можуть використовуватись в `<template>`.

## `v-show` {#v-show}

Ще однією можливістю для умовного показу елементу є директива `v-show`. Використання по своїй суті аналогічне:

```vue-html
<h1 v-show="ok">Привіт!</h1>
```

Різниця полягає в тому, що елемент з `v-show` буде завжди згенерований і лишатиметься в DOM, адже `v-show` лише перемикає CSS властивість `display` елемента.

Варто зазначити, що `v-show` не підтримується елементом `<template>`, та не працює з `v-else`.

## `v-if` проти `v-show` {#v-if-vs-v-show}

`v-if` впливає на "справжній" рендеринг, забезпечуючи, під час перемикання, належне видалення та створення слухачів подій та дочірніх елементів всередині блоків.

`v-if` також є **лінивим**: якщо умова є неправдивою при початковому рендері, він нічого не робитиме — умовний блок не буде згенерований, доки умова вперше не стане правдивою.

`v-show` у порівнянні — елемент завжди згенерований попри початкову умову, завдяки перемиканню лише CSS властивостей.

В цілому, `v-if` має вищу вартість під час перемикання, коли `v-show` має вищу вартість під час початкового рендерингу. Тому надавайте перевагу `v-show`, якщо вам потрібно перемикати щось часто, та `v-if`, якщо умова навряд чи змінюватиметься під час виконання програми.

## `v-if` з `v-for` {#v-if-with-v-for}

::: warning Примітка
**Не** рекомендовано використовувати `v-if` і `v-for` на тому ж самому елементі через їхній неявний пріоритет. Зверніться до [посібника по стилях](/style-guide/rules-essential#avoid-v-if-with-v-for) для деталей.
:::

Коли обидва `v-if` та `v-for` використовуються на тому ж елементі, `v-if` буде обчисленим першим. Перегляньте [Гід по рендерингу списків](list.html#v-for-with-v-if) для деталей.
