# Kết Xuất Danh Sách {#list-rendering}

<div class="options-api">
  <VueSchoolLink href="https://vueschool.io/lessons/list-rendering-in-vue-3" title="Free Vue.js List Rendering Lesson"/>
</div>

<div class="composition-api">
  <VueSchoolLink href="https://vueschool.io/lessons/vue-fundamentals-capi-list-rendering-in-vue" title="Free Vue.js List Rendering Lesson"/>
</div>

## `v-for` {#v-for}

Chúng ta có thể dùng directive `v-for` để kết xuất một danh sách các phần tử dựa trên một mảng. Directive `v-for` yêu cầu cú pháp đặc biệt dạng `item in items`, trong đó `items` là mảng dữ liệu nguồn và `item` là **alias** cho phần tử mảng đang được duyệt qua:

<div class="composition-api">

```js
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])
```

</div>

<div class="options-api">

```js
data() {
  return {
    items: [{ message: 'Foo' }, { message: 'Bar' }]
  }
}
```

</div>

```vue-html
<li v-for="item in items">
  {{ item.message }}
</li>
```

Bên trong phạm vi của `v-for`, các biểu thức template có thể truy cập tất cả các thuộc tính của scope cha. Ngoài ra, `v-for` còn hỗ trợ một alias tùy chọn thứ hai cho chỉ số (index) của phần tử hiện tại:

<div class="composition-api">

```js
const parentMessage = ref('Parent')
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])
```

</div>
<div class="options-api">

```js
data() {
  return {
    parentMessage: 'Parent',
    items: [{ message: 'Foo' }, { message: 'Bar' }]
  }
}
```

</div>

```vue-html
<li v-for="(item, index) in items">
  {{ parentMessage }} - {{ index }} - {{ item.message }}
</li>
```

<script setup>
const parentMessage = 'Parent'
const items = [{ message: 'Foo' }, { message: 'Bar' }]
</script>
<div class="demo">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</div>

<div class="composition-api">

[Thử trong Playground](https://play.vuejs.org/#eNpdTsuqwjAQ/ZVDNlFQu5d64bpwJ7g3LopOJdAmIRlFCPl3p60PcDWcM+eV1X8Iq/uN1FrV6RxtYCTiW/gzzvbBR0ZGpBYFbfQ9tEi1ccadvUuM0ERyvKeUmithMyhn+jCSev4WWaY+vZ7HjH5Sr6F33muUhTR8uW0ThTuJua6mPbJEgGSErmEaENedxX3Z+rgxajbEL2DdhR5zOVOdUSIEDOf8M7IULCHsaPgiMa1eK4QcS6rOSkhdfapVeQLQEWnH)

</div>
<div class="options-api">

[Thử trong Playground](https://play.vuejs.org/#eNpVTssKwjAQ/JUllyr0cS9V0IM3wbvxEOxWAm0a0m0phPy7m1aqhpDsDLMz48XJ2nwaUZSiGp5OWzpKg7PtHUGNjRpbAi8NQK1I7fbrLMkhjc5EJAn4WOXQ0BWHQb2whOS24CSN6qjXhN1Qwt1Dt2kufZ9ASOGXOyvH3GMNCdGdH75VsZVjwGa2VYQRUdVqmLKmdwcpdjEnBW1qnPf8wZIrBQujoff/RSEEyIDZZeGLeCn/dGJyCSlazSZVsUWL8AYme21i)

</div>

Phạm vi biến của `v-for` tương tự đoạn JavaScript sau:

```js
const parentMessage = 'Parent'
const items = [
  /* ... */
]

items.forEach((item, index) => {
  // has access to outer scope `parentMessage`
  // but `item` and `index` are only available in here
  console.log(parentMessage, item.message, index)
})
```

Lưu ý cách giá trị của `v-for` khớp với chữ ký hàm của callback `forEach`. Thực ra, bạn hoàn toàn có thể dùng destructuring trên alias phần tử của `v-for`, tương tự như destructuring tham số hàm:

```vue-html
<li v-for="{ message } in items">
  {{ message }}
</li>

<!-- with index alias -->
<li v-for="({ message }, index) in items">
  {{ message }} {{ index }}
</li>
```

Với `v-for` lồng nhau, phạm vi cũng hoạt động giống như các hàm lồng nhau. Mỗi phạm vi `v-for` có thể truy cập các scope cha:

```vue-html
<li v-for="item in items">
  <span v-for="childItem in item.children">
    {{ item.message }} {{ childItem }}
  </span>
</li>
```

Bạn cũng có thể dùng `of` thay cho `in` làm dấu phân cách, để gần với cú pháp iterator của JavaScript hơn:

```vue-html
<div v-for="item of items"></div>
```

## `v-for` với Object {#v-for-with-an-object}

Bạn cũng có thể dùng `v-for` để duyệt qua các thuộc tính của một object. Thứ tự duyệt sẽ dựa trên kết quả của `Object.values()` khi gọi trên object đó:

<div class="composition-api">

```js
const myObject = reactive({
  title: 'How to do lists in Vue',
  author: 'Jane Doe',
  publishedAt: '2016-04-10'
})
```

</div>
<div class="options-api">

```js
data() {
  return {
    myObject: {
      title: 'How to do lists in Vue',
      author: 'Jane Doe',
      publishedAt: '2016-04-10'
    }
  }
}
```

</div>

```vue-html
<ul>
  <li v-for="value in myObject">
    {{ value }}
  </li>
</ul>
```

Bạn cũng có thể khai báo alias thứ hai cho tên thuộc tính (hay còn gọi là key):

```vue-html
<li v-for="(value, key) in myObject">
  {{ key }}: {{ value }}
</li>
```

Và alias thứ ba cho chỉ số:

```vue-html
<li v-for="(value, key, index) in myObject">
  {{ index }}. {{ key }}: {{ value }}
</li>
```

<div class="composition-api">

[Thử trong Playground](https://play.vuejs.org/#eNo9jjFvgzAQhf/KE0sSCQKpqg7IqRSpQ9WlWycvBC6KW2NbcKaNEP+9B7Tx4nt33917Y3IKYT9ESspE9XVnAqMnjuFZO9MG3zFGdFTVbAbChEvnW2yE32inXe1dz2hv7+dPqhnHO7kdtQPYsKUSm1f/DfZoPKzpuYdx+JAL6cxUka++E+itcoQX/9cO8SzslZoTy+yhODxlxWN2KMR22mmn8jWrpBTB1AZbMc2KVbTyQ56yBkN28d1RJ9uhspFSfNEtFf+GfnZzjP/oOll2NQPjuM4xTftZyIaU5VwuN0SsqMqtWZxUvliq/J4jmX4BTCp08A==)

</div>
<div class="options-api">

[Thử trong Playground](https://play.vuejs.org/#eNo9T8FqwzAM/RWRS1pImnSMHYI3KOwwdtltJ1/cRqXe3Ng4ctYS8u+TbVJjLD3rPelpLg7O7aaARVeI8eS1ozc54M1ZT9DjWQVDMMsBoFekNtucS/JIwQ8RSQI+1/vX8QdP1K2E+EmaDHZQftg/IAu9BaNHGkEP8B2wrFYxgAp0sZ6pn2pAeLepmEuSXDiy7oL9gduXT+3+pW6f631bZoqkJY/kkB6+onnswoDw6owijIhEMByjUBgNU322/lUWm0mZgBX84r1ifz3ettHmupYskjbanedch2XZRcAKTnnvGVIPBpkqGqPTJNGkkaJ5+CiWf4KkfBs=)

</div>

## `v-for` với Phạm Vi Số {#v-for-with-a-range}

`v-for` cũng có thể nhận một số nguyên. Trong trường hợp này, nó sẽ lặp lại template đó nhiều lần, theo phạm vi từ `1...n`.

```vue-html
<span v-for="n in 10">{{ n }}</span>
```

Lưu ý ở đây `n` bắt đầu từ `1` thay vì `0`.

## `v-for` trên `<template>` {#v-for-on-template}

Tương tự như `v-if` trên template, bạn cũng có thể dùng thẻ `<template>` với `v-for` để kết xuất một khối gồm nhiều phần tử. Ví dụ:

```vue-html
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```

## `v-for` kết hợp với `v-if` {#v-for-with-v-if}

Khi cả hai cùng xuất hiện trên một node, `v-if` có độ ưu tiên cao hơn `v-for`. Điều đó có nghĩa là điều kiện của `v-if` sẽ không thể truy cập các biến trong phạm vi của `v-for`:

```vue-html
<!--
This will throw an error because property "todo"
is not defined on instance.
-->
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo.name }}
</li>
```

Cách khắc phục là chuyển `v-for` lên thẻ `<template>` bao ngoài (cách này cũng rõ ràng hơn):

```vue-html
<template v-for="todo in todos">
  <li v-if="!todo.isComplete">
    {{ todo.name }}
  </li>
</template>
```

:::warning Lưu ý
**Không** nên dùng `v-if` và `v-for` trên cùng một phần tử vì thứ tự ưu tiên ngầm định có thể gây nhầm lẫn.

Có hai trường hợp phổ biến dễ khiến bạn muốn làm vậy:

- Để lọc các phần tử trong danh sách (ví dụ `v-for="user in users" v-if="user.isActive"`). Trong trường hợp này, hãy thay `users` bằng một thuộc tính computed mới trả về danh sách đã lọc (ví dụ `activeUsers`).

- Để tránh kết xuất danh sách khi nó cần ẩn (ví dụ `v-for="user in users" v-if="shouldShowUsers"`). Trong trường hợp này, hãy chuyển `v-if` lên phần tử container (ví dụ `ul`, `ol`).
:::

## Duy Trì State với `key` {#maintaining-state-with-key}

Khi Vue cập nhật một danh sách phần tử được kết xuất bằng `v-for`, theo mặc định nó sử dụng chiến lược "vá tại chỗ" (in-place patch). Nếu thứ tự các phần tử dữ liệu thay đổi, thay vì di chuyển các phần tử DOM cho khớp với thứ tự mới, Vue sẽ vá từng phần tử tại chỗ và đảm bảo nó phản ánh đúng nội dung cần kết xuất tại chỉ số đó.

Chế độ mặc định này hiệu quả, nhưng **chỉ phù hợp khi đầu ra kết xuất danh sách của bạn không phụ thuộc vào state của component con hoặc state DOM tạm thời (ví dụ giá trị input trong form)**.

Để giúp Vue xác định danh tính của từng node, từ đó tái sử dụng và sắp xếp lại các phần tử hiện có, bạn cần cung cấp thuộc tính `key` duy nhất cho mỗi phần tử:

```vue-html
<div v-for="item in items" :key="item.id">
  <!-- content -->
</div>
```

Khi dùng `<template v-for>`, `key` nên đặt trên thẻ container `<template>`:

```vue-html
<template v-for="todo in todos" :key="todo.name">
  <li>{{ todo.name }}</li>
</template>
```

:::tip Lưu ý
`key` ở đây là một thuộc tính đặc biệt được bind bằng `v-bind`. Không nhầm lẫn nó với biến key của thuộc tính khi [dùng `v-for` với object](#v-for-with-an-object).
:::

Nên cung cấp thuộc tính `key` cùng với `v-for` bất cứ khi nào có thể, trừ khi nội dung DOM được duyệt đơn giản (tức là không chứa component hay các phần tử DOM có state), hoặc bạn cố ý dựa vào hành vi mặc định để tối ưu hiệu năng.

Binding `key` kỳ vọng các giá trị nguyên thủy — tức là chuỗi và số. Không dùng object làm key cho `v-for`. Để biết chi tiết về cách dùng thuộc tính `key`, hãy xem [tài liệu API về `key`](/api/built-in-special-attributes#key).

## `v-for` với Component {#v-for-with-a-component}

> Mục này yêu cầu kiến thức về [Components](/guide/essentials/component-basics). Bạn có thể bỏ qua và quay lại sau.

Bạn có thể dùng `v-for` trực tiếp trên một component, giống như bất kỳ phần tử thông thường nào (đừng quên cung cấp `key`):

```vue-html
<MyComponent v-for="item in items" :key="item.id" />
```

Tuy nhiên, điều này sẽ không tự động truyền bất kỳ dữ liệu nào vào component, vì component có phạm vi riêng biệt. Để truyền dữ liệu đang được duyệt vào component, chúng ta cần dùng props:

```vue-html
<MyComponent
  v-for="(item, index) in items"
  :item="item"
  :index="index"
  :key="item.id"
/>
```

Lý do không tự động inject `item` vào component là vì điều đó sẽ khiến component bị phụ thuộc chặt chẽ vào cách `v-for` hoạt động. Khai báo rõ ràng nguồn gốc dữ liệu giúp component có thể tái sử dụng trong các tình huống khác.

<div class="composition-api">

Xem [ví dụ về danh sách todo đơn giản](https://play.vuejs.org/#eNp1U8Fu2zAM/RXCGGAHTWx02ylwgxZYB+ywYRhyq3dwLGYRYkuCJTsZjPz7KMmK3ay9JBQfH/meKA/Rk1Jp32G0jnJdtVwZ0Gg6tSkEb5RsDQzQ4h4usG9lAzGVxldoK5n8ZrAZsTQLCduRygAKUUmhDQg8WWyLZwMPtmESx4sAGkL0mH6xrMH+AHC2hvuljw03Na4h/iLBHBAY1wfUbsTFVcwoH28o2/KIIDuaQ0TTlvrwNu/TDe+7PDlKXZ6EZxTiN4kuRI3W0dk4u4yUf7bZfScqw6WAkrEf3m+y8AOcw7Qv6w5T1elDMhs7Nbq7e61gdmme60SQAvgfIhExiSSJeeb3SBukAy1D1aVBezL5XrYN9Csp1rrbNdykqsUehXkookl0EVGxlZHX5Q5rIBLhNHFlbRD6xBiUzlOeuZJQz4XqjI+BxjSSYe2pQWwRBZizV01DmsRWeJA1Qzv0Of2TwldE5hZRlVd+FkbuOmOksJLybIwtkmfWqg+7qz47asXpSiaN3lxikSVwwfC8oD+/sEnV+oh/qcxmU85mebepgLjDBD622Mg+oDrVquYVJm7IEu4XoXKTZ1dho3gnmdJhedEymn9ab3ysDPdc4M9WKp28xE5JbB+rzz/Trm3eK3LAu8/E7p2PNzYM/i3ChR7W7L7hsSIvR7L2Aal1EhqTp80vF95sw3WcG7r8A0XaeME=) để thấy cách kết xuất danh sách các component dùng `v-for`, truyền dữ liệu khác nhau vào mỗi instance.

</div>
<div class="options-api">

Xem [ví dụ về danh sách todo đơn giản](https://play.vuejs.org/#eNqNVE2PmzAQ/SsjVIlEm4C27Qmx0a7UVuqhPVS5lT04eFKsgG2BSVJF+e8d2xhIu10tihR75s2bNx9wiZ60To49RlmUd2UrtNkUUjRatQa2iquvBhvYt6qBOEmDwQbEhQQoJJ4dlOOe9bWBi7WWiuIlStNlcJlYrivr5MywxdIDAVo0fSvDDUDiyeK3eDYZxLGLsI8hI7H9DHeYQuwjeAb3I9gFCFMjUXxSYCoELroKO6fZP17Mf6jev0i1ZQcE1RtHaFrWVW/l+/Ai3zd1clQ1O8k5Uzg+j1HUZePaSFwfvdGhfNIGTaW47bV3Mc6/+zZOfaaslegS18ZE9121mIm0Ep17ynN3N5M8CB4g44AC4Lq8yTFDwAPNcK63kPTL03HR6EKboWtm0N5MvldtA8e1klnX7xphEt3ikTbpoYimsoqIwJY0r9kOa6Ag8lPeta2PvE+cA3M7k6cOEvBC6n7UfVw3imPtQ8eiouAW/IY0mElsiZWqOdqkn5NfCXxB5G6SJRvj05By1xujpJWUp8PZevLUluqP/ajPploLasmk0Re3sJ4VCMnxvKQ//0JMqrID/iaYtSaCz+xudsHjLpPzscVGHYO3SzpdixIXLskK7pcBucnTUdgg3kkmcxhetIrmH4ebr8m/n4jC6FZp+z7HTlLsVx1p4M7odcXPr6+Lnb8YOne5+C2F6/D6DH2Hx5JqOlCJ7yz7IlBTbZsf7vjXVBzjvLDrH5T0lgo=) để thấy cách kết xuất danh sách các component dùng `v-for`, truyền dữ liệu khác nhau vào mỗi instance.

</div>

## Phát Hiện Thay Đổi Mảng {#array-change-detection}

### Phương Thức Thay Đổi Tại Chỗ {#mutation-methods}

Vue có khả năng phát hiện khi các phương thức thay đổi tại chỗ (mutation methods) của mảng phản ứng được gọi và kích hoạt các cập nhật cần thiết. Các phương thức thay đổi tại chỗ đó là:

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

### Thay Thế Mảng {#replacing-an-array}

Các phương thức thay đổi tại chỗ, như tên gọi, sẽ biến đổi trực tiếp mảng gốc mà chúng được gọi trên đó. Ngược lại, cũng có các phương thức không thay đổi tại chỗ như `filter()`, `concat()` và `slice()` — chúng không biến đổi mảng gốc mà **luôn trả về một mảng mới**. Khi làm việc với các phương thức này, chúng ta nên thay thế mảng cũ bằng mảng mới:

<div class="composition-api">

```js
// `items` is a ref with array value
items.value = items.value.filter((item) => item.message.match(/Foo/))
```

</div>
<div class="options-api">

```js
this.items = this.items.filter((item) => item.message.match(/Foo/))
```

</div>

Bạn có thể nghĩ điều này sẽ khiến Vue bỏ đi DOM hiện tại và kết xuất lại toàn bộ danh sách — nhưng may mắn thay, không phải vậy. Vue triển khai một số heuristic thông minh để tối đa hóa việc tái sử dụng phần tử DOM, vì vậy việc thay thế một mảng bằng một mảng khác có các object trùng nhau là một thao tác rất hiệu quả.

## Hiển Thị Kết Quả Đã Lọc/Sắp Xếp {#displaying-filtered-sorted-results}

Đôi khi chúng ta muốn hiển thị phiên bản đã lọc hoặc đã sắp xếp của một mảng mà không thực sự biến đổi hay đặt lại dữ liệu gốc. Trong trường hợp này, bạn có thể tạo một thuộc tính computed trả về mảng đã lọc hoặc đã sắp xếp.

Ví dụ:

<div class="composition-api">

```js
const numbers = ref([1, 2, 3, 4, 5])

const evenNumbers = computed(() => {
  return numbers.value.filter((n) => n % 2 === 0)
})
```

</div>
<div class="options-api">

```js
data() {
  return {
    numbers: [1, 2, 3, 4, 5]
  }
},
computed: {
  evenNumbers() {
    return this.numbers.filter(n => n % 2 === 0)
  }
}
```

</div>

```vue-html
<li v-for="n in evenNumbers">{{ n }}</li>
```

Trong các tình huống không thể dùng thuộc tính computed (ví dụ bên trong các vòng lặp `v-for` lồng nhau), bạn có thể dùng một method:

<div class="composition-api">

```js
const sets = ref([
  [1, 2, 3, 4, 5],
  [6, 7, 8, 9, 10]
])

function even(numbers) {
  return numbers.filter((number) => number % 2 === 0)
}
```

</div>
<div class="options-api">

```js
data() {
  return {
    sets: [[ 1, 2, 3, 4, 5 ], [6, 7, 8, 9, 10]]
  }
},
methods: {
  even(numbers) {
    return numbers.filter(number => number % 2 === 0)
  }
}
```

</div>

```vue-html
<ul v-for="numbers in sets">
  <li v-for="n in even(numbers)">{{ n }}</li>
</ul>
```

Hãy cẩn thận với `reverse()` và `sort()` trong một thuộc tính computed! Hai phương thức này sẽ biến đổi mảng gốc, điều này nên tránh trong các computed getter. Hãy tạo bản sao của mảng gốc trước khi gọi các phương thức này:

```diff
- return numbers.reverse()
+ return [...numbers].reverse()
```
