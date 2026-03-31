# Cú Pháp Template {#template-syntax}

<ScrimbaLink href="https://scrimba.com/links/vue-template-syntax" title="Free Vue.js Template Syntax Lesson" type="scrimba">
  Watch an interactive video lesson on Scrimba
</ScrimbaLink>

Vue sử dụng cú pháp template dựa trên HTML, cho phép bạn khai báo ràng buộc giữa DOM được render và dữ liệu của component instance bên dưới. Tất cả các template Vue đều là HTML hợp lệ về mặt cú pháp, có thể được phân tích bởi các trình duyệt và trình phân tích HTML tuân thủ chuẩn.

Bên dưới, Vue biên dịch các template thành mã JavaScript được tối ưu hóa cao. Kết hợp với hệ thống tính phản ứng, Vue có thể thông minh xác định số lượng component tối thiểu cần render lại và áp dụng số lượng thao tác DOM tối thiểu khi trạng thái ứng dụng thay đổi.

Nếu bạn đã quen với khái niệm Virtual DOM và muốn tận dụng sức mạnh trực tiếp của JavaScript, bạn cũng có thể [viết trực tiếp các hàm render](/guide/extras/render-function) thay vì dùng template, với hỗ trợ JSX tùy chọn. Tuy nhiên, lưu ý rằng chúng không được hưởng mức tối ưu hóa ở thời điểm biên dịch như template.

## Nội Suy Văn Bản {#text-interpolation}

Dạng ràng buộc dữ liệu cơ bản nhất là nội suy văn bản sử dụng cú pháp "Mustache" (dấu ngoặc nhọn kép):

```vue-html
<span>Message: {{ msg }}</span>
```

Thẻ mustache sẽ được thay thế bằng giá trị của thuộc tính `msg` [từ component instance tương ứng](/guide/essentials/reactivity-fundamentals#declaring-reactive-state). Nó cũng sẽ được cập nhật mỗi khi thuộc tính `msg` thay đổi.

## HTML Thô {#raw-html}

Dấu ngoặc nhọn kép diễn giải dữ liệu như văn bản thuần túy, không phải HTML. Để xuất HTML thực sự, bạn cần sử dụng [directive `v-html`](/api/built-in-directives#v-html):

```vue-html
<p>Using text interpolation: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

<script setup>
  const rawHtml = '<span style="color: red">This should be red.</span>'
</script>

<div class="demo">
  <p>Using text interpolation: {{ rawHtml }}</p>
  <p>Using v-html directive: <span v-html="rawHtml"></span></p>
</div>

Ở đây chúng ta gặp một điều mới. Thuộc tính `v-html` mà bạn thấy được gọi là **directive**. Các directive có tiền tố `v-` để chỉ rằng chúng là các thuộc tính đặc biệt do Vue cung cấp, và như bạn có thể đoán được, chúng áp dụng hành vi phản ứng đặc biệt cho DOM được render. Ở đây, về cơ bản chúng ta đang nói "giữ cho nội dung HTML bên trong của phần tử này luôn đồng bộ với thuộc tính `rawHtml` trên instance đang hoạt động hiện tại."

Nội dung của `span` sẽ được thay thế bằng giá trị của thuộc tính `rawHtml`, được diễn giải như HTML thuần túy — các ràng buộc dữ liệu bị bỏ qua. Lưu ý rằng bạn không thể dùng `v-html` để tạo các phần template, vì Vue không phải là engine tạo template dựa trên chuỗi. Thay vào đó, nên dùng component là đơn vị cơ bản để tái sử dụng và tổ hợp UI.

:::warning Cảnh Báo Bảo Mật
Render HTML tùy ý trên trang web của bạn có thể rất nguy hiểm vì dễ dẫn đến [lỗ hổng XSS](https://en.wikipedia.org/wiki/Cross-site_scripting). Chỉ dùng `v-html` trên nội dung đáng tin cậy và **không bao giờ** dùng trên nội dung do người dùng cung cấp.
:::

## Ràng Buộc Thuộc Tính {#attribute-bindings}

Cú pháp Mustache không thể dùng bên trong các thuộc tính HTML. Thay vào đó, hãy dùng [directive `v-bind`](/api/built-in-directives#v-bind):

```vue-html
<div v-bind:id="dynamicId"></div>
```

Directive `v-bind` yêu cầu Vue giữ cho thuộc tính `id` của phần tử đồng bộ với thuộc tính `dynamicId` của component. Nếu giá trị được ràng buộc là `null` hoặc `undefined`, thuộc tính sẽ bị xóa khỏi phần tử được render.

### Cú Pháp Rút Gọn {#shorthand}

Vì `v-bind` được dùng rất phổ biến, nó có một cú pháp rút gọn riêng:

```vue-html
<div :id="dynamicId"></div>
```

Các thuộc tính bắt đầu bằng `:` trông có thể hơi khác so với HTML thông thường, nhưng thực ra đó là ký tự hợp lệ cho tên thuộc tính và tất cả các trình duyệt mà Vue hỗ trợ đều có thể phân tích nó đúng cách. Ngoài ra, chúng không xuất hiện trong markup được render cuối cùng. Cú pháp rút gọn là tùy chọn, nhưng bạn sẽ thấy nó hữu ích khi tìm hiểu thêm về cách dùng sau này.

> Trong phần còn lại của hướng dẫn, chúng tôi sẽ dùng cú pháp rút gọn trong các ví dụ mã, vì đó là cách dùng phổ biến nhất của các lập trình viên Vue.

### Cú Pháp Rút Gọn Cùng Tên {#same-name-shorthand}

- Chỉ hỗ trợ từ 3.4+

Nếu thuộc tính có cùng tên với tên biến của giá trị JavaScript được ràng buộc, cú pháp có thể được rút gọn thêm bằng cách bỏ qua giá trị thuộc tính:

```vue-html
<!-- same as :id="id" -->
<div :id></div>

<!-- this also works -->
<div v-bind:id></div>
```

Điều này tương tự như cú pháp rút gọn thuộc tính khi khai báo đối tượng trong JavaScript. Lưu ý đây là tính năng chỉ có trong Vue 3.4 trở lên.

### Thuộc Tính Boolean {#boolean-attributes}

[Thuộc tính boolean](https://html.spec.whatwg.org/multipage/common-microsyntaxes.html#boolean-attributes) là các thuộc tính có thể biểu thị giá trị đúng/sai thông qua sự hiện diện của chúng trên một phần tử. Ví dụ, [`disabled`](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/disabled) là một trong những thuộc tính boolean được dùng phổ biến nhất.

`v-bind` hoạt động hơi khác trong trường hợp này:

```vue-html
<button :disabled="isButtonDisabled">Button</button>
```

Thuộc tính `disabled` sẽ được thêm vào nếu `isButtonDisabled` có [giá trị truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy). Nó cũng sẽ được thêm vào nếu giá trị là chuỗi rỗng, duy trì tính nhất quán với `<button disabled="">`. Đối với các [giá trị falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) khác, thuộc tính sẽ bị bỏ qua.

### Ràng Buộc Động Nhiều Thuộc Tính {#dynamically-binding-multiple-attributes}

Nếu bạn có một đối tượng JavaScript đại diện cho nhiều thuộc tính như sau:

<div class="composition-api">

```js
const objectOfAttrs = {
  id: 'container',
  class: 'wrapper',
  style: 'background-color:green'
}
```

</div>
<div class="options-api">

```js
data() {
  return {
    objectOfAttrs: {
      id: 'container',
      class: 'wrapper'
    }
  }
}
```

</div>

Bạn có thể ràng buộc tất cả chúng vào một phần tử bằng cách dùng `v-bind` không có đối số:

```vue-html
<div v-bind="objectOfAttrs"></div>
```

## Sử Dụng Biểu Thức JavaScript {#using-javascript-expressions}

Cho đến nay chúng ta chỉ ràng buộc với các khóa thuộc tính đơn giản trong template. Nhưng Vue thực sự hỗ trợ toàn bộ sức mạnh của biểu thức JavaScript bên trong tất cả các ràng buộc dữ liệu:

```vue-html
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div :id="`list-${id}`"></div>
```

Các biểu thức này sẽ được đánh giá như JavaScript trong phạm vi dữ liệu của component instance hiện tại.

Trong các template Vue, biểu thức JavaScript có thể được dùng ở các vị trí sau:

- Bên trong nội suy văn bản (mustache)
- Trong giá trị thuộc tính của bất kỳ directive Vue nào (các thuộc tính đặc biệt bắt đầu bằng `v-`)

### Chỉ Biểu Thức {#expressions-only}

Mỗi ràng buộc chỉ có thể chứa **một biểu thức duy nhất**. Biểu thức là một đoạn mã có thể được đánh giá thành một giá trị. Cách kiểm tra đơn giản là xem liệu nó có thể dùng sau `return` hay không.

Do đó, các ví dụ sau sẽ **KHÔNG** hoạt động:

```vue-html
<!-- this is a statement, not an expression: -->
{{ var a = 1 }}

<!-- flow control won't work either, use ternary expressions -->
{{ if (ok) { return message } }}
```

### Gọi Hàm {#calling-functions}

Có thể gọi một phương thức được component cung cấp bên trong một biểu thức ràng buộc:

```vue-html
<time :title="toTitleDate(date)" :datetime="date">
  {{ formatDate(date) }}
</time>
```

:::tip
Các hàm được gọi bên trong biểu thức ràng buộc sẽ được gọi mỗi khi component cập nhật, vì vậy chúng **không** nên có bất kỳ tác dụng phụ nào, chẳng hạn như thay đổi dữ liệu hoặc kích hoạt các thao tác bất đồng bộ.
:::

### Hạn Chế Truy Cập Biến Toàn Cục {#restricted-globals-access}

Các biểu thức template được sandbox và chỉ có quyền truy cập vào [danh sách giới hạn các biến toàn cục](https://github.com/vuejs/core/blob/main/packages/shared/src/globalsAllowList.ts#L3). Danh sách này cung cấp các biến toàn cục tích hợp thường dùng như `Math` và `Date`.

Các biến toàn cục không nằm trong danh sách trên, ví dụ các thuộc tính gắn vào `window` bởi người dùng, sẽ không thể truy cập được trong biểu thức template. Tuy nhiên, bạn có thể định nghĩa thêm các biến toàn cục cho tất cả biểu thức Vue bằng cách thêm chúng vào [`app.config.globalProperties`](/api/application#app-config-globalproperties).

## Directive {#directives}

Directive là các thuộc tính đặc biệt có tiền tố `v-`. Vue cung cấp một số [directive tích hợp](/api/built-in-directives), bao gồm `v-html` và `v-bind` mà chúng ta đã giới thiệu ở trên.

Giá trị thuộc tính của directive được kỳ vọng là một biểu thức JavaScript duy nhất (ngoại trừ `v-for`, `v-on` và `v-slot`, sẽ được thảo luận trong các phần riêng của chúng). Nhiệm vụ của directive là phản ứng và áp dụng các cập nhật vào DOM khi giá trị của biểu thức thay đổi. Lấy [`v-if`](/api/built-in-directives#v-if) làm ví dụ:

```vue-html
<p v-if="seen">Now you see me</p>
```

Ở đây, directive `v-if` sẽ xóa hoặc chèn phần tử `<p>` dựa trên tính truthy của giá trị biểu thức `seen`.

### Đối Số {#arguments}

Một số directive có thể nhận một "đối số", được biểu thị bằng dấu hai chấm sau tên directive. Ví dụ, directive `v-bind` được dùng để cập nhật phản ứng một thuộc tính HTML:

```vue-html
<a v-bind:href="url"> ... </a>

<!-- shorthand -->
<a :href="url"> ... </a>
```

Ở đây, `href` là đối số, cho directive `v-bind` biết cần ràng buộc thuộc tính `href` của phần tử với giá trị biểu thức `url`. Trong cú pháp rút gọn, mọi thứ trước đối số (tức là `v-bind:`) được rút gọn thành một ký tự duy nhất, `:`.

Một ví dụ khác là directive `v-on`, lắng nghe các sự kiện DOM:

```vue-html
<a v-on:click="doSomething"> ... </a>

<!-- shorthand -->
<a @click="doSomething"> ... </a>
```

Ở đây, đối số là tên sự kiện cần lắng nghe: `click`. `v-on` có cú pháp rút gọn tương ứng là ký tự `@`. Chúng ta cũng sẽ nói về xử lý sự kiện chi tiết hơn sau.

### Đối Số Động {#dynamic-arguments}

Cũng có thể dùng biểu thức JavaScript trong đối số directive bằng cách bọc nó trong dấu ngoặc vuông:

```vue-html
<!--
Note that there are some constraints to the argument expression,
as explained in the "Dynamic Argument Value Constraints" and "Dynamic Argument Syntax Constraints" sections below.
-->
<a v-bind:[attributeName]="url"> ... </a>

<!-- shorthand -->
<a :[attributeName]="url"> ... </a>
```

Ở đây, `attributeName` sẽ được đánh giá động như một biểu thức JavaScript, và giá trị được đánh giá sẽ được dùng làm giá trị cuối cùng cho đối số. Ví dụ, nếu component instance của bạn có thuộc tính dữ liệu `attributeName` với giá trị là `"href"`, thì ràng buộc này sẽ tương đương với `v-bind:href`.

Tương tự, bạn có thể dùng đối số động để ràng buộc một handler với tên sự kiện động:

```vue-html
<a v-on:[eventName]="doSomething"> ... </a>

<!-- shorthand -->
<a @[eventName]="doSomething"> ... </a>
```

Trong ví dụ này, khi giá trị của `eventName` là `"focus"`, `v-on:[eventName]` sẽ tương đương với `v-on:focus`.

#### Ràng Buộc Giá Trị Đối Số Động {#dynamic-argument-value-constraints}

Đối số động được kỳ vọng sẽ đánh giá thành một chuỗi, ngoại trừ `null`. Giá trị đặc biệt `null` có thể được dùng để xóa ràng buộc một cách tường minh. Bất kỳ giá trị không phải chuỗi nào khác sẽ kích hoạt một cảnh báo.

#### Ràng Buộc Cú Pháp Đối Số Động {#dynamic-argument-syntax-constraints}

Các biểu thức đối số động có một số ràng buộc cú pháp vì một số ký tự nhất định, chẳng hạn như dấu cách và dấu nháy, không hợp lệ bên trong tên thuộc tính HTML. Ví dụ, đoạn sau không hợp lệ:

```vue-html
<!-- This will trigger a compiler warning. -->
<a :['foo' + bar]="value"> ... </a>
```

Nếu bạn cần truyền một đối số động phức tạp, tốt hơn nên dùng [thuộc tính computed](./computed), mà chúng ta sẽ đề cập ngay sau đây.

Khi dùng template trong DOM (template được viết trực tiếp trong file HTML), bạn cũng nên tránh đặt tên khóa bằng chữ hoa, vì các trình duyệt sẽ chuyển đổi tên thuộc tính thành chữ thường:

```vue-html
<a :[someAttr]="value"> ... </a>
```

Đoạn trên sẽ được chuyển thành `:[someattr]` trong template trong DOM. Nếu component của bạn có thuộc tính `someAttr` thay vì `someattr`, mã của bạn sẽ không hoạt động. Các template bên trong Single-File Component **không** bị ảnh hưởng bởi ràng buộc này.

### Modifier {#modifiers}

Modifier là các hậu tố đặc biệt được biểu thị bằng dấu chấm, chỉ ra rằng một directive nên được ràng buộc theo một cách đặc biệt. Ví dụ, modifier `.prevent` yêu cầu directive `v-on` gọi `event.preventDefault()` trên sự kiện được kích hoạt:

```vue-html
<form @submit.prevent="onSubmit">...</form>
```

Bạn sẽ thấy các ví dụ khác về modifier sau, [cho `v-on`](./event-handling#event-modifiers) và [cho `v-model`](./forms#modifiers), khi chúng ta khám phá những tính năng đó.

Và cuối cùng, đây là toàn bộ cú pháp directive được hiển thị trực quan:

![directive syntax graph](./images/directive.png)

<!-- https://www.figma.com/file/BGWUknIrtY9HOmbmad0vFr/Directive -->
