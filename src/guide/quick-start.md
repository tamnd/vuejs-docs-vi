---
footer: false
---

<script setup>
import { VTCodeGroup, VTCodeGroupTab } from '@vue/theme'
</script>

# Bắt đầu nhanh {#quick-start}

## Thử Vue trực tuyến {#try-vue-online}

- Bạn có thể thử nhanh Vue trên [Playground](https://play.vuejs.org/#eNo9jcEKwjAMhl/lt5fpQYfXUQfefAMvvRQbddC1pUuHUPrudg4HIcmXjyRZXEM4zYlEJ+T0iEPgXjn6BB8Zhp46WUZWDjCa9f6w9kAkTtH9CRinV4fmRtZ63H20Ztesqiylphqy3R5UYBqD1UyVAPk+9zkvV1CKbCv9poMLiTEfR2/IXpSoXomqZLtti/IFwVtA9A==).

- Nếu muốn dùng HTML thuần, không cần build, có thể dùng [JSFiddle](https://jsfiddle.net/yyx990803/2ke1ab0z/) làm điểm bắt đầu.

- Nếu đã quen với Node.js và build tool, có thể chạy dự án Vue ngay trong trình duyệt qua [StackBlitz](https://vite.new/vue).

- Ngoài ra có thể học theo [hướng dẫn tương tác trên Scrimba](http://scrimba.com/links/vue-quickstart) để biết cách chạy, chỉnh sửa và deploy ứng dụng Vue đầu tiên.

## Tạo ứng dụng Vue {#creating-a-vue-application}

:::tip Điều kiện tiên quyết

- Biết dùng command line
- Đã cài [Node.js](https://nodejs.org/) phiên bản `^20.19.0 || >=22.12.0`
  :::

Ở phần này, bạn sẽ tạo một ứng dụng Vue dạng [SPA](/guide/extras/ways-of-using-vue#single-page-application-spa) chạy trên máy. Dự án dùng [Vite](https://vite.dev/) làm build tool và hỗ trợ [Single-File Component](/guide/scaling-up/sfc) (SFC).

Hãy đảm bảo rằng bạn đã cài phiên bản [Node.js](https://nodejs.org/) mới nhất, và thư mục hiện tại là nơi bạn muốn tạo dự án. Chạy lệnh sau trong command line (không cần gõ ký hiệu `$`):

::: code-group

```sh [npm]
$ npm create vue@latest
```

```sh [pnpm]
$ pnpm create vue@latest
```

```sh [yarn]
# Dành cho Yarn (v1+)
$ yarn create vue

# Dành cho Yarn Modern (v2+)
$ yarn create vue@latest
  
# Dành cho Yarn ^v4.11
$ yarn dlx create-vue@latest
```

```sh [bun]
$ bun create vue@latest
```
:::

Lệnh này sẽ cài đặt và chạy [create-vue](https://github.com/vuejs/create-vue), công cụ tạo dự án chính thức của Vue. Bạn sẽ thấy một số câu hỏi về các tính năng tùy chọn như TypeScript và testing:

<div class="language-sh"><pre><code><span style="color:var(--vt-c-green);">✔</span> <span style="color:#A6ACCD;">Project name: <span style="color:#888;">… <span style="color:#89DDFF;">&lt;</span><span style="color:#888;">your-project-name</span><span style="color:#89DDFF;">&gt;</span></span></span>
<span style="color:var(--vt-c-green);">✔</span> <span style="color:#A6ACCD;">Add TypeScript? <span style="color:#888;">… <span style="color:#89DDFF;text-decoration:underline">No</span> / Yes</span></span>
<span style="color:var(--vt-c-green);">✔</span> <span style="color:#A6ACCD;">Add JSX Support? <span style="color:#888;">… <span style="color:#89DDFF;text-decoration:underline">No</span> / Yes</span></span>
<span style="color:var(--vt-c-green);">✔</span> <span style="color:#A6ACCD;">Add Vue Router for Single Page Application development? <span style="color:#888;">… <span style="color:#89DDFF;text-decoration:underline">No</span> / Yes</span></span>
<span style="color:var(--vt-c-green);">✔</span> <span style="color:#A6ACCD;">Add Pinia for state management? <span style="color:#888;">… <span style="color:#89DDFF;text-decoration:underline">No</span> / Yes</span></span>
<span style="color:var(--vt-c-green);">✔</span> <span style="color:#A6ACCD;">Add Vitest for Unit testing? <span style="color:#888;">… <span style="color:#89DDFF;text-decoration:underline">No</span> / Yes</span></span>
<span style="color:var(--vt-c-green);">✔</span> <span style="color:#A6ACCD;">Add an End-to-End Testing Solution? <span style="color:#888;">… <span style="color:#89DDFF;text-decoration:underline">No</span> / Cypress / Nightwatch / Playwright</span></span>
<span style="color:var(--vt-c-green);">✔</span> <span style="color:#A6ACCD;">Add ESLint for code quality? <span style="color:#888;">… No / <span style="color:#89DDFF;text-decoration:underline">Yes</span></span></span>
<span style="color:var(--vt-c-green);">✔</span> <span style="color:#A6ACCD;">Add Prettier for code formatting? <span style="color:#888;">… <span style="color:#89DDFF;text-decoration:underline">No</span> / Yes</span></span>
<span style="color:var(--vt-c-green);">✔</span> <span style="color:#A6ACCD;">Add Vue DevTools 7 extension for debugging? (experimental) <span style="color:#888;">… <span style="color:#89DDFF;text-decoration:underline">No</span> / Yes</span></span>
<span></span>
<span style="color:#A6ACCD;">Scaffolding project in ./<span style="color:#89DDFF;">&lt;</span><span style="color:#888;">your-project-name</span><span style="color:#89DDFF;">&gt;</span>...</span>
<span style="color:#A6ACCD;">Done.</span></code></pre></div>

Nếu chưa chắc về tùy chọn nào, bạn có thể tạm thời chọn `No` bằng cách nhấn Enter. Sau khi tạo xong dự án, hãy làm theo hướng dẫn để cài đặt dependencies và khởi động dev server:

::: code-group

```sh-vue [npm]
$ cd {{'<your-project-name>'}}
$ npm install
$ npm run dev
```

```sh-vue [pnpm]
$ cd {{'<your-project-name>'}}
$ pnpm install
$ pnpm run dev
```

```sh-vue [yarn]
$ cd {{'<your-project-name>'}}
$ yarn
$ yarn dev
```

```sh-vue [bun]
$ cd {{'<your-project-name>'}}
$ bun install
$ bun run dev
```

:::


Giờ bạn đã chạy được project Vue đầu tiên trên máy. Lưu ý là các component mẫu trong project được tạo sẵn dùng [Composition API](/guide/introduction#composition-api) cùng với `<script setup>`, thay vì [Options API](/guide/introduction#options-api).

Một vài điểm bạn nên biết thêm:

- IDE khuyến nghị là [Visual Studio Code](https://code.visualstudio.com/) + [Vue - Official extension](https://marketplace.visualstudio.com/items?itemName=Vue.volar). Nếu bạn dùng editor khác, hãy xem phần [hỗ trợ IDE](/guide/scaling-up/tooling#ide-support).
- Chi tiết hơn về công cụ phát triển, bao gồm cả tích hợp với các backend framework, được trình bày trong [Hướng dẫn công cụ](/guide/scaling-up/tooling).
- Để hiểu thêm về Vite, build tool nền tảng phía sau, hãy xem [tài liệu Vite](https://vite.dev/).
- Nếu bạn chọn sử dụng TypeScript, hãy xem [Hướng dẫn sử dụng TypeScript](/guide/typescript/overview).

Khi bạn sẵn sàng đưa ứng dụng lên production, hãy chạy lệnh sau:

::: code-group

```sh [npm]
$ npm run build
```

```sh [pnpm]
$ pnpm run build
```

```sh [yarn]
$ yarn build
```

```sh [bun]
$ bun run build
```

:::


Lệnh này sẽ tạo ra bản build sẵn sàng cho production của ứng dụng trong thư mục `./dist` của dự án. Hãy xem [Hướng dẫn triển khai production](/guide/best-practices/production-deployment) để tìm hiểu thêm về cách đưa ứng dụng lên production.

[Các bước tiếp theo >](#next-steps)

## Dùng Vue từ CDN {#using-vue-from-cdn}

Bạn có thể dùng Vue trực tiếp từ CDN thông qua một thẻ script:

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

Ở đây chúng ta dùng [unpkg](https://unpkg.com/), nhưng bạn cũng có thể dùng bất kỳ CDN nào phân phối package npm, ví dụ như [jsdelivr](https://www.jsdelivr.com/package/npm/vue) hoặc [cdnjs](https://cdnjs.com/libraries/vue). Tất nhiên, bạn cũng có thể tải file này về và tự phục vụ (serve).

Khi dùng Vue từ CDN, sẽ không có "bước build" nào cả. Điều này giúp thiết lập đơn giản hơn nhiều và phù hợp để bổ sung vào HTML tĩnh hoặc tích hợp với backend framework. Tuy nhiên, bạn sẽ không thể sử dụng cú pháp Single-File Component (SFC).

### Dùng bản build global {#using-the-global-build}

Liên kết phía trên tải _global build_ của Vue, nơi tất cả API cấp cao nhất được expose dưới dạng thuộc tính trên object toàn cục `Vue`. Dưới đây là ví dụ đầy đủ sử dụng global build:

<div class="options-api">

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app">{{ message }}</div>

<script>
  const { createApp } = Vue

  createApp({
    data() {
      return {
        message: 'Xin chào Vue!'
      }
    }
  }).mount('#app')
</script>
```

[Demo trên CodePen >](https://codepen.io/vuejs-examples/pen/QWJwJLp)

</div>

<div class="composition-api">

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app">{{ message }}</div>

<script>
  const { createApp, ref } = Vue

  createApp({
    setup() {
      const message = ref('Xin chào Vue!')
      return {
        message
      }
    }
  }).mount('#app')
</script>
```

[Demo trên CodePen >](https://codepen.io/vuejs-examples/pen/eYQpQEG)

:::tip
Rất nhiều ví dụ về Composition API trong phần hướng dẫn sẽ dùng cú pháp `<script setup>`, vốn yêu cầu build tool. Nếu bạn muốn dùng Composition API mà không có bước build, hãy tham khảo cách dùng [`setup()` option](/api/composition-api-setup).
:::

</div>

### Dùng bản build ES modules {#using-the-es-module-build}

Trong phần còn lại của tài liệu, chúng tôi sẽ chủ yếu sử dụng cú pháp [ES modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules). Hầu hết các trình duyệt hiện đại ngày nay đã hỗ trợ ES modules, vì vậy chúng ta có thể dùng Vue từ CDN thông qua ES modules như sau:

<div class="options-api">

```html{3,4}
<div id="app">{{ message }}</div>

<script type="module">
  import { createApp } from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'

  createApp({
    data() {
      return {
        message: 'Xin chào Vue!'
      }
    }
  }).mount('#app')
</script>
```

</div>

<div class="composition-api">

```html{3,4}
<div id="app">{{ message }}</div>

<script type="module">
  import { createApp, ref } from 'https://unpkg.com/vue@3/dist/vue.esm-browser.js'

  createApp({
    setup() {
      const message = ref('Xin chào Vue!')
      return {
        message
      }
    }
  }).mount('#app')
</script>
```

</div>

Lưu ý rằng ở đây chúng ta đang dùng `<script type="module">`, và URL CDN được import vào đang trỏ tới **bản build ES modules** của Vue.

<div class="options-api">

[Demo trên CodePen >](https://codepen.io/vuejs-examples/pen/VwVYVZO)

</div>
<div class="composition-api">

[Demo trên CodePen >](https://codepen.io/vuejs-examples/pen/MWzazEv)

</div>

### Bật Import Maps {#enabling-import-maps}

Trong ví dụ ở trên, chúng ta import từ URL CDN đầy đủ, nhưng ở phần còn lại của tài liệu bạn sẽ thấy đoạn code như thế này:

```js
import { createApp } from 'vue'
```

Chúng ta có thể chỉ cho trình duyệt biết vị trí của import `vue` bằng [Import Maps](https://caniuse.com/import-maps):

<div class="options-api">

```html{1-7,12}
<script type="importmap">
  {
    "imports": {
      "vue": "https://unpkg.com/vue@3/dist/vue.esm-browser.js"
    }
  }
</script>

<div id="app">{{ message }}</div>

<script type="module">
  import { createApp } from 'vue'

  createApp({
    data() {
      return {
        message: 'Xin chào Vue!'
      }
    }
  }).mount('#app')
</script>
```

[Demo trên CodePen >](https://codepen.io/vuejs-examples/pen/wvQKQyM)

</div>

<div class="composition-api">

```html{1-7,12}
<script type="importmap">
  {
    "imports": {
      "vue": "https://unpkg.com/vue@3/dist/vue.esm-browser.js"
    }
  }
</script>

<div id="app">{{ message }}</div>

<script type="module">
  import { createApp, ref } from 'vue'

  createApp({
    setup() {
      const message = ref('Xin chào Vue!')
      return {
        message
      }
    }
  }).mount('#app')
</script>
```

[Demo trên CodePen >](https://codepen.io/vuejs-examples/pen/YzRyRYM)

</div>

Bạn cũng có thể thêm các dependency khác vào import map, miễn là chúng trỏ tới phiên bản ES module của thư viện tương ứng.

:::tip Hỗ trợ Import Maps trên trình duyệt
Import Maps là một tính năng còn khá mới. Bạn nên kiểm tra xem trình duyệt mình đang dùng có nằm trong [danh sách hỗ trợ](https://caniuse.com/import-maps) hay không. Lưu ý rằng Safari chỉ hỗ trợ từ phiên bản 16.4 trở lên.
:::

:::warning Lưu ý khi dùng trong production
Các ví dụ trên đang sử dụng bản development của Vue. Nếu bạn dùng Vue qua CDN trong môi trường production, hãy chuyển sang bản build tối ưu và tham khảo [Hướng dẫn triển khai production](/guide/best-practices/production-deployment#without-build-tools).

Dù có thể dùng Vue mà không cần hệ thống build, bạn cũng có thể cân nhắc [`vuejs/petite-vue`](https://github.com/vuejs/petite-vue) cho các trường hợp đơn giản. Cách tiếp cận này phù hợp với những bối cảnh trước đây thường dùng [`jquery/jquery`](https://github.com/jquery/jquery), hoặc hiện nay là [`alpinejs/alpine`](https://github.com/alpinejs/alpine).
:::

### Tách các module {#splitting-up-the-modules}

Khi dự án phức tạp hơn, bạn nên tách code thành các file JavaScript riêng để dễ quản lý và bảo trì. Ví dụ:

```html [index.html]
<div id="app"></div>

<script type="module">
  import { createApp } from 'vue'
  import MyComponent from './my-component.js'

  createApp(MyComponent).mount('#app')
</script>
```

<div class="options-api">

```js [my-component.js]
export default {
  data() {
    return { count: 0 }
  },
  template: `<div>Số đếm là: {{ count }}</div>`
}
```

</div>
<div class="composition-api">

```js [my-component.js]
import { ref } from 'vue'
export default {
  setup() {
    const count = ref(0)
    return { count }
  },
  template: `<div>Số đếm là: {{ count }}</div>`
}
```

</div>

Nếu bạn mở trực tiếp file `index.html` trên trình duyệt, bạn sẽ gặp lỗi vì ES modules không hoạt động qua giao thức `file://`, đây là giao thức mà trình duyệt dùng khi mở file local.

Vì lý do bảo mật, ES modules chỉ hoạt động qua giao thức `http://`, đây cũng là giao thức mà trình duyệt sử dụng khi tải các trang web. Để ES modules chạy được trên máy local, bạn cần chạy file `index.html` thông qua `http://` bằng một HTTP server local.

Để khởi động HTTP server local, trước tiên hãy đảm bảo bạn đã cài đặt [Node.js](https://nodejs.org/en/), sau đó chạy lệnh `npx serve` trong command line tại thư mục chứa file HTML. Bạn cũng có thể dùng bất kỳ HTTP server nào khác, miễn là có thể chạy các file tĩnh với MIME type chính xác.

Bạn có thể nhận thấy template của component được import đang được viết trực tiếp dưới dạng một chuỗi JavaScript. Nếu bạn dùng VS Code, có thể cài extension [es6-string-html](https://marketplace.visualstudio.com/items?itemName=Tobermory.es6-string-html) và thêm comment `/*html*/` trước chuỗi để bật tô màu cú pháp cho phần HTML bên trong chuỗi đó.

## Các bước tiếp theo {#next-steps}

Nếu bạn đã bỏ qua phần [Giới thiệu](/guide/introduction), chúng tôi đặc biệt khuyến nghị bạn đọc nó trước khi tiếp tục với phần còn lại của tài liệu.

<div class="vt-box-container next-steps">
  <a class="vt-box" href="/guide/essentials/application.html">
    <p class="next-steps-link">Tiếp tục với phần hướng dẫn</p>
    <p class="next-steps-caption">Phần hướng dẫn sẽ đưa bạn đi qua từng khía cạnh của framework một cách đầy đủ và chi tiết.</p>
  </a>
  <a class="vt-box" href="/tutorial/">
    <p class="next-steps-link">Thử phần hướng dẫn tương tác</p>
    <p class="next-steps-caption">Dành cho những ai thích học bằng cách trực tiếp thực hành.</p>
  </a>
  <a class="vt-box" href="/examples/">
    <p class="next-steps-link">Xem các ví dụ</p>
    <p class="next-steps-caption">Khám phá các ví dụ về những tính năng cốt lõi và các tác vụ UI phổ biến.</p>
  </a>
</div>
