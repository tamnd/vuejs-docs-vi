# Xử Lý Sự Kiện {#event-handling}

<div class="options-api">
  <VueSchoolLink href="https://vueschool.io/lessons/user-events-in-vue-3" title="Free Vue.js Events Lesson"/>
</div>

<div class="composition-api">
  <VueSchoolLink href="https://vueschool.io/lessons/vue-fundamentals-capi-user-events-in-vue-3" title="Free Vue.js Events Lesson"/>
</div>

## Lắng Nghe Sự Kiện {#listening-to-events}

Chúng ta có thể dùng directive `v-on`, thường được viết tắt thành ký hiệu `@`, để lắng nghe các sự kiện DOM và thực thi một đoạn JavaScript khi chúng được kích hoạt. Cú pháp đầy đủ là `v-on:click="handler"`, hoặc dùng cú pháp rút gọn: `@click="handler"`.

Giá trị của handler có thể là một trong hai dạng:

1. **Inline handler:** JavaScript được thực thi trực tiếp khi sự kiện xảy ra (tương tự thuộc tính `onclick` của HTML thuần).

2. **Method handler:** Tên hoặc đường dẫn của một phương thức được định nghĩa trên component.

## Inline Handler {#inline-handlers}

Inline handler thường được dùng trong các trường hợp đơn giản, ví dụ:

<div class="composition-api">

```js
const count = ref(0)
```

</div>
<div class="options-api">

```js
data() {
  return {
    count: 0
  }
}
```

</div>

```vue-html
<button @click="count++">Add 1</button>
<p>Count is: {{ count }}</p>
```

<div class="composition-api">

[Thử trong Playground](https://play.vuejs.org/#eNo9jssKgzAURH/lko0tgrbbEqX+Q5fZaLxiqHmQ3LgJ+fdqFZcD58xMYp1z1RqRvRgP0itHEJCia4VR2llPkMDjBBkmbzUUG1oII4y0JhBIGw2hh2Znbo+7MLw+WjZ/C4TaLT3hnogPkcgaeMtFyW8j2GmXpWBtN47w5PWBHLhrPzPCKfWDXRHmPsCAaOBfgSOkdH3IGUhpDBWv9/e8vsZZ/gFFhFJN)

</div>
<div class="options-api">

[Thử trong Playground](https://play.vuejs.org/#eNo9jcEKgzAQRH9lyKlF0PYqqdR/6DGXaLYo1RjiRgrivzepIizLzu7sm1XUzuVLIFEKObe+d1wpS183eYahtw4DY1UWMJr15ZpmxYAnDt7uF0BxOwXL5Evc0kbxlmyxxZLFyY2CaXSDZkqKZROYJ4tnO/Tt56HEgckyJaraGNxlsVt2u6teHeF40s20EDo9oyGy+CPIYF1xULBt4H6kOZeFiwBZnOFi+wH0B1hk)

</div>

## Method Handler {#method-handlers}

Tuy nhiên, logic của nhiều event handler sẽ phức tạp hơn và không thể viết gọn trong một inline handler. Đó là lý do `v-on` cũng có thể nhận tên hoặc đường dẫn của một phương thức trên component mà bạn muốn gọi.

Ví dụ:

<div class="composition-api">

```js
const name = ref('Vue.js')

function greet(event) {
  alert(`Hello ${name.value}!`)
  // `event` is the native DOM event
  if (event) {
    alert(event.target.tagName)
  }
}
```

</div>
<div class="options-api">

```js
data() {
  return {
    name: 'Vue.js'
  }
},
methods: {
  greet(event) {
    // `this` inside methods points to the current active instance
    alert(`Hello ${this.name}!`)
    // `event` is the native DOM event
    if (event) {
      alert(event.target.tagName)
    }
  }
}
```

</div>

```vue-html
<!-- `greet` is the name of the method defined above -->
<button @click="greet">Greet</button>
```

<div class="composition-api">

[Thử trong Playground](https://play.vuejs.org/#eNpVj0FLxDAQhf/KMwjtXtq7dBcFQS/qzVMOrWFao2kSkkkvpf/dJIuCEBgm771vZnbx4H23JRJ3YogqaM+IxMlfpNWrd4GxI9CMA3NwK5psbaSVVjkbGXZaCediaJv3RN1XbE5FnZNVrJ3FEoi4pY0sn7BLC0yGArfjMxnjcLsXQrdNJtFxM+Ys0PcYa2CEjuBPylNYb4THtxdUobj0jH/YX3D963gKC5WyvGZ+xR7S5jf01yPzeblhWr2ZmErHw0dizivfK6PV91mKursUl6dSh/4qZ+vQ/+XE8QODonDi)

</div>
<div class="options-api">

[Thử trong Playground](https://play.vuejs.org/#eNplUE1LxDAQ/StjEbYL0t5LXRQEvag3Tz00prNtNE1CMilC6X83SUkRhJDJfLz3Jm8tHo2pFo9FU7SOW2Ho0in8MdoSDHhlXhKsnQIYGLHyvL8BLJK3KmcAis3YwOnDY/XlTnt1i2G7i/eMNOnBNRkwWkQqcUFFByVAXUNPk3A9COXEgBkGRgtFDkgDTQjcWxuAwDiJBeMsMcUxszCJlsr+BaXUcLtGwiqut930579KST1IBd5Aqlgie3p/hdTIk+IK//bMGqleEbMjxjC+BZVDIv0+m9CpcNr6MDgkhLORjDBm1H56Iq3ggUvBv++7IhnUFZfnGNt6b4fRtj5wxfYL9p+Sjw==)

</div>

Method handler tự động nhận đối tượng sự kiện DOM gốc đã kích hoạt nó — trong ví dụ trên, chúng ta có thể truy cập phần tử phát ra sự kiện thông qua `event.target`.

<div class="composition-api">

Xem thêm: [Typing Event Handlers](/guide/typescript/composition-api#typing-event-handlers) <sup class="vt-badge ts" />

</div>
<div class="options-api">

Xem thêm: [Typing Event Handlers](/guide/typescript/options-api#typing-event-handlers) <sup class="vt-badge ts" />

</div>

### Phân Biệt Method Handler và Inline Handler {#method-vs-inline-detection}

Trình biên dịch template phân biệt method handler bằng cách kiểm tra xem chuỗi giá trị của `v-on` có phải là một định danh JavaScript hợp lệ hay một đường dẫn truy cập thuộc tính hay không. Chẳng hạn, `foo`, `foo.bar` và `foo['bar']` được coi là method handler, trong khi `foo()` và `count++` được coi là inline handler.

## Gọi Phương Thức Trong Inline Handler {#calling-methods-in-inline-handlers}

Thay vì gắn trực tiếp vào tên phương thức, chúng ta cũng có thể gọi phương thức trong một inline handler. Cách này cho phép chúng ta truyền đối số tùy chỉnh vào phương thức thay vì chỉ dùng đối tượng sự kiện gốc:

<div class="composition-api">

```js
function say(message) {
  alert(message)
}
```

</div>
<div class="options-api">

```js
methods: {
  say(message) {
    alert(message)
  }
}
```

</div>

```vue-html
<button @click="say('hello')">Say hello</button>
<button @click="say('bye')">Say bye</button>
```

<div class="composition-api">

[Thử trong Playground](https://play.vuejs.org/#eNp9jTEOwjAMRa8SeSld6I5CBWdg9ZJGBiJSN2ocpKjq3UmpFDGx+Vn//b/ANYTjOxGcQEc7uyAqkqTQI98TW3ETq2jyYaQYzYNatSArZTzNUn/IK7Ludr2IBYTG4I3QRqKHJFJ6LtY7+zojbIXNk7yfmhahv5msvqS7PfnHGjJVp9w/hu7qKKwfEd1NSg==)

</div>
<div class="options-api">

[Thử trong Playground](https://play.vuejs.org/#eNptjUEKwjAQRa8yZFO7sfsSi57B7WzGdjTBtA3NVC2ldzehEFwIw8D7vM9f1cX742tmVSsd2sl6aXDgjx8ngY7vNDuBFQeAnsWMXagToQAEWg49h0APLncDAIUcT5LzlKJsqRBfPF3ljQjCvXcknEj0bRYZBzi3zrbPE6o0UBhblKiaKy1grK52J/oA//23IcmNBD8dXeVBtX0BF0pXsg==)

</div>

## Truy Cập Đối Số Sự Kiện Trong Inline Handler {#accessing-event-argument-in-inline-handlers}

Đôi khi chúng ta cũng cần truy cập sự kiện DOM gốc trong một inline handler. Bạn có thể truyền nó vào phương thức bằng biến đặc biệt `$event`, hoặc dùng một arrow function inline:

```vue-html
<!-- using $event special variable -->
<button @click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>

<!-- using inline arrow function -->
<button @click="(event) => warn('Form cannot be submitted yet.', event)">
  Submit
</button>
```

<div class="composition-api">

```js
function warn(message, event) {
  // now we have access to the native event
  if (event) {
    event.preventDefault()
  }
  alert(message)
}
```

</div>
<div class="options-api">

```js
methods: {
  warn(message, event) {
    // now we have access to the native event
    if (event) {
      event.preventDefault()
    }
    alert(message)
  }
}
```

</div>

## Event Modifier {#event-modifiers}

Một nhu cầu rất phổ biến là gọi `event.preventDefault()` hoặc `event.stopPropagation()` bên trong event handler. Mặc dù chúng ta có thể thực hiện điều này dễ dàng trong các phương thức, nhưng sẽ tốt hơn nếu các phương thức chỉ tập trung vào logic dữ liệu mà không cần xử lý các chi tiết sự kiện DOM.

Để giải quyết vấn đề này, Vue cung cấp **event modifier** cho `v-on`. Modifier là các hậu tố của directive, được biểu thị bằng dấu chấm.

- `.stop`
- `.prevent`
- `.self`
- `.capture`
- `.once`
- `.passive`

```vue-html
<!-- the click event's propagation will be stopped -->
<a @click.stop="doThis"></a>

<!-- the submit event will no longer reload the page -->
<form @submit.prevent="onSubmit"></form>

<!-- modifiers can be chained -->
<a @click.stop.prevent="doThat"></a>

<!-- just the modifier -->
<form @submit.prevent></form>

<!-- only trigger handler if event.target is the element itself -->
<!-- i.e. not from a child element -->
<div @click.self="doThat">...</div>
```

::: tip
Thứ tự rất quan trọng khi dùng modifier vì code tương ứng được tạo ra theo đúng thứ tự đó. Do đó, `@click.prevent.self` sẽ chặn **hành vi mặc định của click trên cả phần tử lẫn các phần tử con**, trong khi `@click.self.prevent` chỉ chặn hành vi mặc định của click trên chính phần tử đó.
:::

Các modifier `.capture`, `.once` và `.passive` tương ứng với [các tùy chọn của phương thức `addEventListener` gốc](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener#options):

```vue-html
<!-- use capture mode when adding the event listener     -->
<!-- i.e. an event targeting an inner element is handled -->
<!-- here before being handled by that element           -->
<div @click.capture="doThis">...</div>

<!-- the click event will be triggered at most once -->
<a @click.once="doThis"></a>

<!-- the scroll event's default behavior (scrolling) will happen -->
<!-- immediately, instead of waiting for `onScroll` to complete  -->
<!-- in case it contains `event.preventDefault()`                -->
<div @scroll.passive="onScroll">...</div>
```

Modifier `.passive` thường được dùng với các event listener cảm ứng để [cải thiện hiệu suất trên thiết bị di động](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener#improving_scroll_performance_using_passive_listeners).

::: tip
Không dùng `.passive` và `.prevent` cùng nhau, vì `.passive` đã báo hiệu cho trình duyệt rằng bạn _không_ có ý định chặn hành vi mặc định của sự kiện. Nếu dùng đồng thời, bạn có thể nhận được cảnh báo từ trình duyệt.
:::

## Key Modifier {#key-modifiers}

Khi lắng nghe các sự kiện bàn phím, chúng ta thường cần kiểm tra phím cụ thể nào được nhấn. Vue cho phép thêm key modifier cho `v-on` hoặc `@` khi lắng nghe sự kiện phím:

```vue-html
<!-- only call `submit` when the `key` is `Enter` -->
<input @keyup.enter="submit" />
```

Bạn có thể dùng trực tiếp bất kỳ tên phím hợp lệ nào được cung cấp qua [`KeyboardEvent.key`](https://developer.mozilla.org/en-US/docs/Web/API/UI_Events/Keyboard_event_key_values) làm modifier bằng cách chuyển chúng sang dạng kebab-case.

```vue-html
<input @keyup.page-down="onPageDown" />
```

Trong ví dụ trên, handler chỉ được gọi khi `$event.key` bằng `'PageDown'`.

### Alias Phím {#key-aliases}

Vue cung cấp alias cho các phím được dùng phổ biến nhất:

- `.enter`
- `.tab`
- `.delete` (bắt cả phím "Delete" lẫn "Backspace")
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

### Modifier Phím Hệ Thống {#system-modifier-keys}

Bạn có thể dùng các modifier sau để chỉ kích hoạt event listener cho chuột hoặc bàn phím khi phím modifier tương ứng đang được giữ:

- `.ctrl`
- `.alt`
- `.shift`
- `.meta`

::: tip Lưu ý
Trên bàn phím Macintosh, meta là phím command (⌘). Trên bàn phím Windows, meta là phím Windows (⊞). Trên bàn phím Sun Microsystems, meta được đánh dấu bằng hình thoi đặc (◆). Trên một số bàn phím nhất định, đặc biệt là bàn phím MIT và Lisp machine cùng các phiên bản kế thừa như Knight keyboard, space-cadet keyboard, meta được ghi nhãn là "META". Trên bàn phím Symbolics, meta được ghi nhãn là "META" hoặc "Meta".
:::

Ví dụ:

```vue-html
<!-- Alt + Enter -->
<input @keyup.alt.enter="clear" />

<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
```

::: tip
Lưu ý rằng các phím modifier khác với các phím thông thường, và khi dùng với sự kiện `keyup`, chúng phải đang được giữ khi sự kiện phát ra. Nói cách khác, `keyup.ctrl` chỉ kích hoạt khi bạn nhả một phím khác trong khi đang giữ `ctrl`. Nó sẽ không kích hoạt nếu bạn chỉ nhả đúng phím `ctrl`.
:::

### Modifier `.exact` {#exact-modifier}

Modifier `.exact` cho phép kiểm soát tổ hợp modifier hệ thống chính xác cần thiết để kích hoạt sự kiện.

```vue-html
<!-- this will fire even if Alt or Shift is also pressed -->
<button @click.ctrl="onClick">A</button>

<!-- this will only fire when Ctrl and no other keys are pressed -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- this will only fire when no system modifiers are pressed -->
<button @click.exact="onClick">A</button>
```

## Modifier cho Nút Chuột {#mouse-button-modifiers}

- `.left`
- `.right`
- `.middle`

Các modifier này giới hạn handler chỉ phản hồi với sự kiện được kích hoạt bởi một nút chuột cụ thể.

Tuy nhiên cần lưu ý, tên các modifier `.left`, `.right` và `.middle` dựa trên bố cục chuột thuận tay phải thông thường, nhưng thực ra chúng lần lượt đại diện cho các loại trigger sự kiện thiết bị trỏ là "chính", "phụ" và "bổ trợ" — chứ không phải các nút vật lý cụ thể. Vì vậy, với chuột dành cho tay trái, nút "chính" có thể về mặt vật lý nằm ở bên phải nhưng vẫn kích hoạt handler của modifier `.left`. Hoặc một trackpad có thể kích hoạt handler `.left` bằng một ngón tay, handler `.right` bằng hai ngón và handler `.middle` bằng ba ngón. Tương tự, các thiết bị khác và nguồn sự kiện tạo ra sự kiện "chuột" có thể có các chế độ kích hoạt không liên quan gì đến "trái" hay "phải".
