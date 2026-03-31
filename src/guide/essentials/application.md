# Tạo một Ứng dụng Vue {#creating-a-vue-application}

## Instance Ứng Dụng {#the-application-instance}

Mọi ứng dụng Vue đều bắt đầu bằng cách tạo một **instance ứng dụng** mới thông qua hàm [`createApp`](/api/application#createapp):

```js
import { createApp } from 'vue'

const app = createApp({
  /* root component options */
})
```

## Component Gốc {#the-root-component}

Đối tượng chúng ta truyền vào `createApp` thực chất là một component. Mỗi ứng dụng cần có một "component gốc" có thể chứa các component khác như là con của nó.

Nếu bạn đang dùng Single-File Component, chúng ta thường import component gốc từ một file riêng:

```js
import { createApp } from 'vue'
// import the root component App from a single-file component.
import App from './App.vue'

const app = createApp(App)
```

Dù nhiều ví dụ trong hướng dẫn này chỉ cần một component duy nhất, hầu hết các ứng dụng thực tế đều được tổ chức thành một cây gồm các component lồng nhau và có thể tái sử dụng. Ví dụ, cây component của một ứng dụng Todo có thể trông như sau:

```
App (root component)
├─ TodoList
│  └─ TodoItem
│     ├─ TodoDeleteButton
│     └─ TodoEditButton
└─ TodoFooter
   ├─ TodoClearButton
   └─ TodoStatistics
```

Ở các phần sau của hướng dẫn, chúng ta sẽ thảo luận về cách định nghĩa và kết hợp nhiều component lại với nhau. Trước đó, hãy tập trung vào những gì xảy ra bên trong một component đơn lẻ.

## Mount Ứng Dụng {#mounting-the-app}

Một instance ứng dụng sẽ không render bất cứ thứ gì cho đến khi phương thức `.mount()` được gọi. Nó nhận một đối số "container", có thể là một phần tử DOM thực sự hoặc một chuỗi selector:

```html
<div id="app"></div>
```

```js
app.mount('#app')
```

Nội dung của component gốc trong ứng dụng sẽ được render bên trong phần tử chứa. Bản thân phần tử chứa đó không được coi là một phần của ứng dụng.

Phương thức `.mount()` luôn phải được gọi sau khi tất cả các cấu hình và đăng ký tài nguyên của ứng dụng đã hoàn tất. Cũng lưu ý rằng giá trị trả về của nó, khác với các phương thức đăng ký tài nguyên, là instance của component gốc chứ không phải instance ứng dụng.

### Template Component Gốc Trong DOM {#in-dom-root-component-template}

Template của component gốc thường là một phần của chính component đó, nhưng cũng có thể cung cấp template riêng biệt bằng cách viết trực tiếp bên trong phần tử chứa khi mount:

```html
<div id="app">
  <button @click="count++">{{ count }}</button>
</div>
```

```js
import { createApp } from 'vue'

const app = createApp({
  data() {
    return {
      count: 0
    }
  }
})

app.mount('#app')
```

Vue sẽ tự động sử dụng `innerHTML` của phần tử chứa làm template nếu component gốc chưa có tùy chọn `template`.

Template trong DOM thường được dùng trong các ứng dụng [sử dụng Vue không có bước build](/guide/quick-start.html#using-vue-from-cdn). Chúng cũng có thể được dùng kết hợp với các framework phía server, nơi template gốc có thể được server tạo ra động.

## Cấu Hình Ứng Dụng {#app-configurations}

Instance ứng dụng cung cấp một đối tượng `.config` cho phép chúng ta cấu hình một số tùy chọn ở cấp ứng dụng, ví dụ như định nghĩa một trình xử lý lỗi ở cấp ứng dụng để bắt các lỗi từ tất cả các component con:

```js
app.config.errorHandler = (err) => {
  /* handle error */
}
```

Instance ứng dụng cũng cung cấp một số phương thức để đăng ký tài nguyên có phạm vi toàn ứng dụng. Ví dụ, đăng ký một component:

```js
app.component('TodoDeleteButton', TodoDeleteButton)
```

Điều này giúp `TodoDeleteButton` có thể sử dụng ở bất kỳ đâu trong ứng dụng của chúng ta. Chúng ta sẽ thảo luận về việc đăng ký component và các loại tài nguyên khác ở các phần sau của hướng dẫn. Bạn cũng có thể xem danh sách đầy đủ các API của instance ứng dụng trong [tài liệu API](/api/application).

Hãy đảm bảo áp dụng tất cả các cấu hình ứng dụng trước khi mount ứng dụng!

## Nhiều Instance Ứng Dụng {#multiple-application-instances}

Bạn không bị giới hạn ở một instance ứng dụng duy nhất trên cùng một trang. API `createApp` cho phép nhiều ứng dụng Vue cùng tồn tại trên một trang, mỗi ứng dụng có phạm vi riêng về cấu hình và tài nguyên toàn cục:

```js
const app1 = createApp({
  /* ... */
})
app1.mount('#container-1')

const app2 = createApp({
  /* ... */
})
app2.mount('#container-2')
```

Nếu bạn đang dùng Vue để cải thiện HTML do server render và chỉ cần Vue kiểm soát các phần cụ thể của một trang lớn, hãy tránh mount một instance ứng dụng Vue duy nhất lên toàn bộ trang. Thay vào đó, hãy tạo nhiều instance ứng dụng nhỏ và mount chúng lên các phần tử mà chúng phụ trách.
