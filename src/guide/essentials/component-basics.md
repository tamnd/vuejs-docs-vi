# Căn Bản về Component {#components-basics}

<ScrimbaLink href="https://scrimba.com/links/vue-component-basics" title="Free Vue.js Components Basics Lesson" type="scrimba">
  Xem bài học video tương tác trên Scrimba
</ScrimbaLink>

Component cho phép chúng ta chia nhỏ giao diện thành các phần độc lập, có thể tái sử dụng, và xử lý từng phần một cách riêng biệt. Một ứng dụng thường được tổ chức thành một cây component lồng nhau:

![Component Tree](./images/components.png)

<!-- https://www.figma.com/file/qa7WHDQRWuEZNRs7iZRZSI/components -->

Cách tổ chức này rất giống với cách chúng ta lồng các phần tử HTML gốc, nhưng Vue triển khai mô hình component riêng của mình cho phép đóng gói nội dung và logic tùy chỉnh trong mỗi component. Vue cũng hoạt động tốt với Web Components gốc. Nếu bạn tò mò về mối quan hệ giữa Vue Components và Web Components gốc, hãy [tìm hiểu thêm tại đây](/guide/extras/web-components).

## Định Nghĩa một Component {#defining-a-component}

Khi sử dụng bước build, chúng ta thường định nghĩa mỗi Vue component trong một file riêng với phần mở rộng `.vue` — được gọi là [Single-File Component](/guide/scaling-up/sfc) (viết tắt là SFC):

<div class="options-api">

```vue
<script>
export default {
  data() {
    return {
      count: 0
    }
  }
}
</script>

<template>
  <button @click="count++">You clicked me {{ count }} times.</button>
</template>
```

</div>
<div class="composition-api">

```vue
<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <button @click="count++">You clicked me {{ count }} times.</button>
</template>
```

</div>

Khi không sử dụng bước build, một Vue component có thể được định nghĩa dưới dạng một đối tượng JavaScript thuần chứa các tùy chọn đặc trưng của Vue:

<div class="options-api">

```js
export default {
  data() {
    return {
      count: 0
    }
  },
  template: `
    <button @click="count++">
      You clicked me {{ count }} times.
    </button>`
}
```

</div>
<div class="composition-api">

```js
import { ref } from 'vue'

export default {
  setup() {
    const count = ref(0)
    return { count }
  },
  template: `
    <button @click="count++">
      You clicked me {{ count }} times.
    </button>`
  // Can also target an in-DOM template:
  // template: '#my-template-element'
}
```

</div>

Template ở đây được nhúng trực tiếp dưới dạng chuỗi JavaScript, và Vue sẽ biên dịch nó khi chạy. Bạn cũng có thể dùng ID selector trỏ tới một phần tử (thường là các phần tử `<template>` gốc) — Vue sẽ lấy nội dung của phần tử đó làm nguồn template.

Ví dụ trên định nghĩa một component duy nhất và xuất nó làm export mặc định của file `.js`, nhưng bạn cũng có thể dùng named export để xuất nhiều component từ cùng một file.

## Sử Dụng một Component {#using-a-component}

:::tip
Trong phần còn lại của hướng dẫn này, chúng ta sẽ sử dụng cú pháp SFC — các khái niệm về component đều giống nhau dù bạn có sử dụng bước build hay không. Phần [Ví dụ](/examples/) trình bày cách sử dụng component trong cả hai trường hợp.
:::

Để sử dụng một component con, chúng ta cần import nó vào component cha. Giả sử chúng ta đặt component đếm số lần nhấp vào file `ButtonCounter.vue`, component đó sẽ được export mặc định từ file:

<div class="options-api">

```vue
<script>
import ButtonCounter from './ButtonCounter.vue'

export default {
  components: {
    ButtonCounter
  }
}
</script>

<template>
  <h1>Here is a child component!</h1>
  <ButtonCounter />
</template>
```

Để component được import hiển thị trong template, chúng ta cần [đăng ký](/guide/components/registration) nó thông qua tùy chọn `components`. Component sau đó sẽ dùng được dưới dạng tag với tên đã đăng ký.

</div>

<div class="composition-api">

```vue
<script setup>
import ButtonCounter from './ButtonCounter.vue'
</script>

<template>
  <h1>Here is a child component!</h1>
  <ButtonCounter />
</template>
```

Với `<script setup>`, các component được import sẽ tự động có thể dùng trong template mà không cần đăng ký thêm.

</div>

Bạn cũng có thể đăng ký component ở phạm vi toàn cục, giúp nó dùng được ở tất cả các component trong ứng dụng mà không cần import từng lần. Ưu và nhược điểm của đăng ký toàn cục so với đăng ký cục bộ được thảo luận trong phần [Đăng Ký Component](/guide/components/registration).

Component có thể được tái sử dụng bao nhiêu lần tùy thích:

```vue-html
<h1>Here are many child components!</h1>
<ButtonCounter />
<ButtonCounter />
<ButtonCounter />
```

<div class="options-api">

[Try it in the Playground](https://play.vuejs.org/#eNqVUE1LxDAQ/StjLqusNHotcfHj4l8QcontLBtsJiGdiFL6301SdrEqyEJyeG9m3ps3k3gIoXlPKFqhxi7awDtN1gUfGR4Ts6cnn4gxwj56B5tGrtgyutEEoAk/6lCPe5MGhqmwnc9KhMRjuxCwFi3UrCk/JU/uGTC6MBjGglgdbnfPGBFM/s7QJ3QHO/TfxC+UzD21d72zPItU8uQrrsWvnKsT/ZW2N2wur45BI3KKdETlFlmphZsF58j/RgdQr3UJuO8G273daVFFtlstahngxSeoNezBIUzTYgPzDGwdjk1VkYvMj4jzF0nwsyQ=)

</div>
<div class="composition-api">

[Try it in the Playground](https://play.vuejs.org/#eNqVj91KAzEQhV/lmJsqlY3eSlr8ufEVhNys6ZQGNz8kE0GWfXez2SJUsdCLuZiZM9+ZM4qnGLvPQuJBqGySjYxMXOJWe+tiSIznwhz8SyieKWGfgsOqkyfTGbDSXsmFUG9rw+Ti0DPNHavD/faVEqGv5Xr/BXOwww4mVBNPnvOVklXTtKeO8qKhkj++4lb8+fL/mCMS7TEdAy6BtDfBZ65fVgA2s+L67uZMUEC9N0s8msGaj40W7Xa91qKtgbdQ0Ha0gyOM45E+TWDrKHeNIhfMr0DTN4U0me8=)

</div>

Hãy chú ý rằng khi nhấp vào các nút, mỗi nút duy trì `count` riêng của nó. Đó là vì mỗi lần bạn sử dụng một component, một **instance** mới của nó sẽ được tạo ra.

Trong SFC, nên dùng tên tag theo kiểu `PascalCase` cho các component con để phân biệt với các phần tử HTML gốc. Mặc dù tên tag HTML gốc không phân biệt hoa thường, Vue SFC là định dạng được biên dịch nên có thể dùng tên tag phân biệt hoa thường. Chúng ta cũng có thể dùng `/>` để đóng tag.

Nếu bạn viết template trực tiếp trong DOM (ví dụ: nội dung của phần tử `<template>` gốc), template sẽ tuân theo hành vi phân tích HTML gốc của trình duyệt. Trong trường hợp đó, bạn phải dùng `kebab-case` và thẻ đóng tường minh cho các component:

```vue-html
<!-- if this template is written in the DOM -->
<button-counter></button-counter>
<button-counter></button-counter>
<button-counter></button-counter>
```

Xem [các lưu ý khi phân tích template trong DOM](#in-dom-template-parsing-caveats) để biết thêm chi tiết.

## Truyền Props {#passing-props}

Nếu chúng ta xây dựng một blog, chúng ta có thể cần một component đại diện cho một bài viết. Chúng ta muốn tất cả các bài viết có cùng bố cục giao diện nhưng nội dung khác nhau. Component như vậy sẽ không hữu ích trừ khi bạn có thể truyền dữ liệu vào nó, chẳng hạn như tiêu đề và nội dung của bài viết cụ thể cần hiển thị. Đó là lúc props phát huy tác dụng.

Props là các thuộc tính tùy chỉnh mà bạn có thể đăng ký trên một component. Để truyền tiêu đề vào component bài viết blog, chúng ta cần khai báo nó trong danh sách props mà component chấp nhận, sử dụng <span class="options-api">tùy chọn [`props`](/api/options-state#props)</span><span class="composition-api">macro [`defineProps`](/api/sfc-script-setup#defineprops-defineemits)</span>:

<div class="options-api">

```vue [BlogPost.vue]
<script>
export default {
  props: ['title']
}
</script>

<template>
  <h4>{{ title }}</h4>
</template>
```

Khi một giá trị được truyền vào thuộc tính prop, nó sẽ trở thành thuộc tính trên instance của component đó. Giá trị này có thể truy cập được trong template và trong ngữ cảnh `this` của component, giống như bất kỳ thuộc tính component nào khác.

</div>
<div class="composition-api">

```vue [BlogPost.vue]
<script setup>
defineProps(['title'])
</script>

<template>
  <h4>{{ title }}</h4>
</template>
```

`defineProps` là một compile-time macro chỉ dùng được bên trong `<script setup>` và không cần import tường minh. Các props đã khai báo sẽ tự động hiển thị trong template. `defineProps` cũng trả về một đối tượng chứa tất cả các props được truyền vào component, để chúng ta có thể truy cập chúng trong JavaScript khi cần:

```js
const props = defineProps(['title'])
console.log(props.title)
```

Xem thêm: [Typing Component Props](/guide/typescript/composition-api#typing-component-props) <sup class="vt-badge ts" />

Nếu bạn không dùng `<script setup>`, props nên được khai báo bằng tùy chọn `props`, và đối tượng props sẽ được truyền vào `setup()` như là đối số đầu tiên:

```js
export default {
  props: ['title'],
  setup(props) {
    console.log(props.title)
  }
}
```

</div>

Một component có thể có bao nhiêu props tùy thích và mặc định, bất kỳ giá trị nào cũng có thể được truyền vào bất kỳ prop nào.

Sau khi prop được đăng ký, bạn có thể truyền dữ liệu vào nó như một thuộc tính tùy chỉnh, như thế này:

```vue-html
<BlogPost title="My journey with Vue" />
<BlogPost title="Blogging with Vue" />
<BlogPost title="Why Vue is so fun" />
```

Tuy nhiên, trong một ứng dụng thực tế, bạn thường sẽ có một mảng bài viết trong component cha:

<div class="options-api">

```js
export default {
  // ...
  data() {
    return {
      posts: [
        { id: 1, title: 'My journey with Vue' },
        { id: 2, title: 'Blogging with Vue' },
        { id: 3, title: 'Why Vue is so fun' }
      ]
    }
  }
}
```

</div>
<div class="composition-api">

```js
const posts = ref([
  { id: 1, title: 'My journey with Vue' },
  { id: 2, title: 'Blogging with Vue' },
  { id: 3, title: 'Why Vue is so fun' }
])
```

</div>

Sau đó muốn render một component cho từng bài, sử dụng `v-for`:

```vue-html
<BlogPost
  v-for="post in posts"
  :key="post.id"
  :title="post.title"
 />
```

<div class="options-api">

[Try it in the Playground](https://play.vuejs.org/#eNp9UU1rhDAU/CtDLrawVfpxklRo74We2kPtQdaoaTUJ8bmtiP+9ia6uC2VBgjOZeXnz3sCejAkPnWAx4+3eSkNJqmRjtCU817p81S2hsLpBEEYL4Q1BqoBUid9Jmosi62rC4Nm9dn4lFLXxTGAt5dG482eeUXZ1vdxbQZ1VCwKM0zr3x4KBATKPcbsDSapFjOClx5d2JtHjR1KFN9fTsfbWcXdy+CZKqcqL+vuT/r3qvQqyRatRdMrpF/nn/DNhd7iPR+v8HCDRmDoj4RHxbfyUDjeFto8p8yEh1Rw2ZV4JxN+iP96FMvest8RTTws/gdmQ8HUr7ikere+yHduu62y//y3NWG38xIOpeODyXcoE8OohGYZ5VhhHHjl83sD4B3XgyGI=)

</div>
<div class="composition-api">

[Try it in the Playground](https://play.vuejs.org/#eNp9kU9PhDAUxL/KpBfWBCH+OZEuid5N9qSHrQezFKhC27RlDSF8d1tYQBP1+N78OpN5HciD1sm54yQj1J6M0A6Wu07nTIpWK+MwwPASI0qjWkQejVbpsVHVQVl30ZJ0WQRHjwFMnpT0gPZLi32w2h2DMEAUGW5iOOEaniF66vGuOiN5j0/hajx7B4zxxt5ubIiphKz+IO828qXugw5hYRXKTnqSydcrJmk61/VF/eB4q5s3x8Pk6FJjauDO16Uye0ZCBwg5d2EkkED2wfuLlogibMOTbMpf9tMwP8jpeiMfRdM1l8Tk+/F++Y6Cl0Lyg1Ha7o7R5Bn9WwSg9X0+DPMxMI409fPP1PELlVmwdQ==)

</div>

Hãy chú ý cách [cú pháp `v-bind`](/api/built-in-directives#v-bind) (`:title="post.title"`) được dùng để truyền giá trị prop động. Điều này đặc biệt hữu ích khi bạn chưa biết trước nội dung cụ thể cần render.

Đó là tất cả những gì bạn cần biết về props hiện tại, nhưng sau khi đọc xong trang này và cảm thấy thoải mái với nội dung, chúng tôi khuyến khích bạn quay lại để đọc hướng dẫn đầy đủ về [Props](/guide/components/props).

## Lắng Nghe Sự Kiện {#listening-to-events}

Khi phát triển component `<BlogPost>`, một số tính năng có thể cần giao tiếp ngược lại với component cha. Ví dụ, chúng ta có thể muốn thêm tính năng trợ năng để phóng to cỡ chữ của các bài viết, trong khi giữ nguyên phần còn lại của trang ở kích thước mặc định.

Ở component cha, chúng ta có thể hỗ trợ tính năng này bằng cách thêm <span class="options-api">thuộc tính data</span><span class="composition-api">ref</span> `postFontSize`:

<div class="options-api">

```js{6}
data() {
  return {
    posts: [
      /* ... */
    ],
    postFontSize: 1
  }
}
```

</div>
<div class="composition-api">

```js{5}
const posts = ref([
  /* ... */
])

const postFontSize = ref(1)
```

</div>

Có thể dùng trong template để kiểm soát cỡ chữ của tất cả bài viết:

```vue-html{1,7}
<div :style="{ fontSize: postFontSize + 'em' }">
  <BlogPost
    v-for="post in posts"
    :key="post.id"
    :title="post.title"
   />
</div>
```

Bây giờ hãy thêm một nút vào template của component `<BlogPost>`:

```vue{5} [BlogPost.vue]
<!-- omitting <script> -->
<template>
  <div class="blog-post">
    <h4>{{ title }}</h4>
    <button>Enlarge text</button>
  </div>
</template>
```

Nút này hiện chưa làm gì — chúng ta muốn khi nhấp nút, component con thông báo cho component cha rằng nó nên phóng to cỡ chữ của tất cả bài viết. Để giải quyết vấn đề này, component cung cấp hệ thống custom event. Component cha có thể lắng nghe bất kỳ sự kiện nào trên instance của component con bằng `v-on` hoặc `@`, giống như với DOM event gốc:

```vue-html{3}
<BlogPost
  ...
  @enlarge-text="postFontSize += 0.1"
 />
```

Sau đó, component con có thể phát ra sự kiện trên chính nó bằng cách gọi [phương thức **`$emit`**](/api/component-instance#emit) tích hợp sẵn, truyền tên của sự kiện:

```vue{5} [BlogPost.vue]
<!-- omitting <script> -->
<template>
  <div class="blog-post">
    <h4>{{ title }}</h4>
    <button @click="$emit('enlarge-text')">Enlarge text</button>
  </div>
</template>
```

Nhờ có listener `@enlarge-text="postFontSize += 0.1"`, component cha sẽ nhận được sự kiện và cập nhật giá trị của `postFontSize`.

<div class="options-api">

[Try it in the Playground](https://play.vuejs.org/#eNqNUsFOg0AQ/ZUJMaGNbbHqidCmmujNxMRED9IDhYWuhV0CQy0S/t1ZYIEmaiRkw8y8N/vmMZVxl6aLY8EM23ByP+Mprl3Bk1RmCPexjJ5ljhBmMgFzYemEIpiuAHAFOzXQgIVeESNUKutL4gsmMLfbBPStVFTP1Bl46E2mup4xLDKhI4CUsMR+1zFABTywYTkD5BgzG8ynEj4kkVgJnxz38Eqaut5jxvXAUCIiLqI/8TcD/m1fKhTwHHIJYSEIr+HbnqikPkqBL/yLSMs23eDooNexel8pQJaksYeMIgAn4EewcyxjtnKNCsK+zbgpXILJEnW30bCIN7ZTPcd5KDNqoWjARWufa+iyfWBlV13wYJRvJtWVJhiKGyZiL4vYHNkJO8wgaQVXi6UGr51+Ndq5LBqMvhyrH9eYGePtOVu3n3YozWSqFsBsVJmt3SzhzVaYY2nm9l82+7GX5zTGjlTM1SyNmy5SeX+7rqr2r0NdOxbFXWVXIEoBGz/m/oHIF0rB5Pz6KTV6aBOgEo7Vsn51ov4GgAAf2A==)

</div>
<div class="composition-api">

[Try it in the Playground](https://play.vuejs.org/#eNp1Uk1PwkAQ/SuTxqQYgYp6ahaiJngzITHRA/UAZQor7W7TnaK16X93th8UEuHEvPdm5s3bls5Tmo4POTq+I0yYyZTAIOXpLFAySXVGUEKGEVQQZToBl6XukXqO9XahDbXc2OsAO5FlAIEKtWJByqCBqR01WFqiBLnxYTIEkhSjD+5rAV86zxQW8C1pB+88Aaphr73rtXbNVqrtBeV9r/zYFZYHacBoiHLFykB9Xgfq1NmLVvQmf7E1OGFaeE0anAMXhEkarwhtRWIjD+AbKmKcBk4JUdvtn8+6ARcTu87hLuCf6NJpSoDDKNIZj7BtIFUTUuB0tL/HomXHcnOC18d1TF305COqeJVtcUT4Q62mtzSF2/GkE8/E8b1qh8Ljw/if8I7nOkPn9En/+Ug2GEmFi0ynZrB0azOujbfB54kki5+aqumL8bING28Yr4xh+2vePrI39CnuHmZl2TwwVJXwuG6ZdU6kFTyGsQz33HyFvH5wvvyaB80bACwgvKbrYgLVH979DQc=)

</div>

Chúng ta có thể tùy chọn khai báo các sự kiện được phát ra bằng <span class="options-api">tùy chọn [`emits`](/api/options-state#emits)</span><span class="composition-api">macro [`defineEmits`](/api/sfc-script-setup#defineprops-defineemits)</span>:

<div class="options-api">

```vue{4} [BlogPost.vue]
<script>
export default {
  props: ['title'],
  emits: ['enlarge-text']
}
</script>
```

</div>
<div class="composition-api">

```vue{3} [BlogPost.vue]
<script setup>
defineProps(['title'])
defineEmits(['enlarge-text'])
</script>
```

</div>

Điều này giúp ghi lại tất cả các sự kiện mà một component phát ra và tùy chọn [xác thực chúng](/guide/components/events#events-validation). Nó cũng giúp Vue tránh áp dụng ngầm định chúng như là native listener trên phần tử gốc của component con.

<div class="composition-api">

Tương tự `defineProps`, `defineEmits` chỉ dùng được trong `<script setup>` và không cần import. Nó trả về một hàm `emit` tương đương với phương thức `$emit`. Có thể dùng hàm này để phát sự kiện trong phần `<script setup>` của component, nơi `$emit` không trực tiếp truy cập được:

```vue
<script setup>
const emit = defineEmits(['enlarge-text'])

emit('enlarge-text')
</script>
```

Xem thêm: [Typing Component Emits](/guide/typescript/composition-api#typing-component-emits) <sup class="vt-badge ts" />

Nếu bạn không dùng `<script setup>`, bạn có thể khai báo các sự kiện bằng tùy chọn `emits`. Bạn có thể truy cập hàm `emit` như một thuộc tính của setup context (được truyền vào `setup()` như là đối số thứ hai):

```js
export default {
  emits: ['enlarge-text'],
  setup(props, ctx) {
    ctx.emit('enlarge-text')
  }
}
```

</div>

Đó là tất cả những gì bạn cần biết về custom event của component hiện tại, nhưng sau khi đọc xong trang này và cảm thấy thoải mái với nội dung, chúng tôi khuyến khích bạn quay lại để đọc hướng dẫn đầy đủ về [Custom Events](/guide/components/events).

## Phân Phối Nội Dung với Slot {#content-distribution-with-slots}

Giống như với các phần tử HTML, việc truyền nội dung vào một component thường rất hữu ích, như thế này:

```vue-html
<AlertBox>
  Something bad happened.
</AlertBox>
```

Kết quả có thể trông như thế này:

:::danger This is an Error for Demo Purposes
Something bad happened.
:::

Điều này có thể thực hiện được bằng cách sử dụng phần tử `<slot>` tùy chỉnh của Vue:

```vue{4} [AlertBox.vue]
<template>
  <div class="alert-box">
    <strong>This is an Error for Demo Purposes</strong>
    <slot />
  </div>
</template>

<style scoped>
.alert-box {
  /* ... */
}
</style>
```

Như bạn thấy ở trên, chúng ta dùng `<slot>` như một chỗ giữ chỗ (placeholder) cho nội dung cần hiển thị — và chỉ vậy thôi. Xong rồi!

<div class="options-api">

[Try it in the Playground](https://play.vuejs.org/#eNpVUcFOwzAM/RUTDruwFhCaUCmThsQXcO0lbbKtIo0jx52Kpv07TreWouTynl+en52z2oWQnXqrClXGhtrA28q3XUBi2DlL/IED7Ak7WGX5RKQHq8oDVN4Oo9TYve4dwzmxDcp7bz3HAs5/LpfKyy3zuY0Atl1wmm1CXE5SQeLNX9hZPrb+ALU2cNQhWG9NNkrnLKIt89lGPahlyDTVogVAadoTNE7H+F4pnZTrGodKjUUpRyb0h+0nEdKdRL3CW7GmfNY5ZLiiMhfP/ynG0SL/OAuxwWCNMNncbVqSQyrgfrPZvCVcIxkrxFMYIKJrDZA1i8qatGl72ehLGEY6aGNkNwU8P96YWjffB8Lem/Xkvn9NR6qy+fRd14FSgopvmtQmzTT9Toq9VZdfIpa5jQ==)

</div>
<div class="composition-api">

[Try it in the Playground](https://play.vuejs.org/#eNpVUEtOwzAQvcpgFt3QBBCqUAiRisQJ2GbjxG4a4Xis8aQKqnp37PyUyqv3mZn3fBVH55JLr0Umcl9T6xi85t4VpW07h8RwNJr4Cwc4EXawS9KFiGO70ubpNBcmAmDdOSNZR8T5Yg0IoOQf7DSfW9tAJRWcpXPaapWM1nVt8ObpukY8ie29GHNzAiBX7QVqI73/LIWMzn2FQylGMcieCW1TfBMhPYSoE5zFitLVZ5BhQnkadt6nGKt5/jMafI1Oq8Ak6zW4xrEaDVIGj4fD4SPiCknpQLy4ATyaVgFptVH2JFXb+wze3DDSTioV/iaD1+eZqWT92xD2Vu2X7af3+IJ6G7/UToVigpJnTzwTO42eWDnELsTtH/wUqH4=)

</div>

Đó là tất cả những gì bạn cần biết về slot hiện tại, nhưng sau khi đọc xong trang này và cảm thấy thoải mái với nội dung, chúng tôi khuyến khích bạn quay lại để đọc hướng dẫn đầy đủ về [Slot](/guide/components/slots).

## Component Động {#dynamic-components}

Đôi khi, việc chuyển đổi linh hoạt giữa các component rất hữu ích, chẳng hạn như trong giao diện tab:

<div class="options-api">

[Open example in the Playground](https://play.vuejs.org/#eNqNVE2PmzAQ/Ssj9kArLSHbrXpwk1X31mMPvS17cIxJrICNbJMmivLfO/7AEG2jRiDkefP85sNmztlr3y8OA89ItjJMi96+VFJ0vdIWfqqOQ6NVB/midIYj5sn9Sxlrkt9b14RXzXbiMElEO5IAKsmPnljzhg6thbNDmcLdkktrSADAJ/IYlj5MXEc9Z1w8VFNLP30ed2luBy1HC4UHrVH2N90QyJ1kHnUALN1gtLeIQu6juEUMkb8H5sXHqiS+qzK1Cw3Lu76llqMFsKrFAVhLjVlXWc07VWUeR89msFbhhhAWDkWjNJIwPgjp06iy5CV7fgrOOTgKv+XoKIIgpnoGyiymSmZ1wnq9dqJweZ8p/GCtYHtUmBMdLXFitgDnc9ju68b0yxDO1WzRTEcFRLiUJsEqSw3wwi+rMpFDj0psEq5W5ax1aBp7at1y4foWzq5R0hYN7UR7ImCoNIXhWjTfnW+jdM01gaf+CEa1ooYHzvnMVWhaiwEP90t/9HBP61rILQJL3POMHw93VG+FLKzqUYx3c2yjsOaOwNeRO2B8zKHlzBKQWJNH1YHrplV/iiMBOliFILYNK5mOKdSTMviGCTyNojFdTKBoeWNT3s8f/Vpsd7cIV61gjHkXnotR6OqVkJbrQKdsv9VqkDWBh2bpnn8VXaDcHPexE4wFzsojO9eDUOSVPF+65wN/EW7sHRsi5XaFqaexn+EH9Xcpe8zG2eWG3O0/NVzUaeJMk+jGhUXlNPXulw5j8w7t2bi8X32cuf/Vv/wF/SL98A==)

</div>
<div class="composition-api">

[Open example in the Playground](https://play.vuejs.org/#eNqNVMGOmzAQ/ZURe2BXCiHbrXpwk1X31mMPvS1V5RiTWAEb2SZNhPLvHdvggLZRE6TIM/P8/N5gpk/e2nZ57HhCkrVhWrQWDLdd+1pI0bRKW/iuGg6VVg2ky9wFDp7G8g9lrIl1H80Bb5rtxfFKMcRzUA+aV3AZQKEEhWRKGgus05pL+5NuYeNwj6mTkT4VckRYujVY63GT17twC6/Fr4YjC3kp5DoPNtEgBpY3bU0txwhgXYojsJoasymSkjeqSHweK9vOWoUbXIC/Y1YpjaDH3wt39hMI6TUUSYSQAz8jArPT5Mj+nmIhC6zpAu1TZlEhmXndbBwpXH5NGL6xWrADMsyaMj1lkAzQ92E7mvYe8nCcM24xZApbL5ECiHCSnP73KyseGnvh6V/XedwS2pVjv3C1ziddxNDYc+2WS9fC8E4qJW1W0UbUZwKGSpMZrkX11dW2SpdcE3huT2BULUp44JxPSpmmpegMgU/tyadbWpZC7jCxwj0v+OfTDdU7ITOrWiTjzTS3Vei8IfB5xHZ4PmqoObMEJHryWXXkuqrVn+xEgHZWYRKbh06uLyv4iQq+oIDnkXSQiwKymlc26n75WNdit78FmLWCMeZL+GKMwlKrhLRcBzhlh51WnSwJPFQr9/zLdIZ007w/O6bR4MQe2bseBJMzer5yzwf8MtzbOzYMkNsOY0+HfoZv1d+lZJGMg8fNqdsfbbio4b77uRVv7I0Li8xxZN1PHWbeHdyTWXc/+zgw/8t/+QsROe9h)

</div>

Tính năng trên được thực hiện nhờ phần tử `<component>` của Vue với thuộc tính đặc biệt `is`:

<div class="options-api">

```vue-html
<!-- Component changes when currentTab changes -->
<component :is="currentTab"></component>
```

</div>
<div class="composition-api">

```vue-html
<!-- Component changes when currentTab changes -->
<component :is="tabs[currentTab]"></component>
```

</div>

Trong ví dụ trên, giá trị được truyền vào `:is` có thể là:

- chuỗi tên của một component đã đăng ký, HOẶC
- đối tượng component đã được import thực sự

Bạn cũng có thể dùng thuộc tính `is` để tạo các phần tử HTML thông thường.

Khi chuyển đổi giữa nhiều component với `<component :is="...">`, một component sẽ bị unmount khi bị chuyển đi. Chúng ta có thể buộc các component không hoạt động ở trạng thái "còn sống" với [component `<KeepAlive>`](/guide/built-ins/keep-alive) tích hợp sẵn.

## Các Lưu Ý Khi Phân Tích Template Trong DOM {#in-dom-template-parsing-caveats}

Nếu bạn viết Vue template trực tiếp trong DOM, Vue sẽ phải lấy chuỗi template từ DOM. Điều này dẫn đến một số lưu ý do hành vi phân tích HTML gốc của trình duyệt.

:::tip
Cần lưu ý rằng các hạn chế được thảo luận dưới đây chỉ áp dụng nếu bạn viết template trực tiếp trong DOM. Chúng KHÔNG áp dụng nếu bạn sử dụng string template từ các nguồn sau:

- Single-File Components
- Chuỗi template nội tuyến (ví dụ: `template: '...'`)
- `<script type="text/x-template">`
  :::

### Không Phân Biệt Hoa Thường {#case-insensitivity}

Tên tag và thuộc tính HTML không phân biệt hoa thường, vì vậy trình duyệt sẽ hiểu mọi ký tự viết hoa là viết thường. Điều đó có nghĩa là khi dùng template trong DOM, tên component theo PascalCase và tên prop theo camelCase hay tên sự kiện `v-on` đều cần chuyển sang dạng kebab-case (dùng gạch nối) tương đương:

```js
// camelCase in JavaScript
const BlogPost = {
  props: ['postTitle'],
  emits: ['updatePost'],
  template: `
    <h3>{{ postTitle }}</h3>
  `
}
```

```vue-html
<!-- kebab-case in HTML -->
<blog-post post-title="hello!" @update-post="onUpdatePost"></blog-post>
```

### Thẻ Tự Đóng {#self-closing-tags}

Trong các đoạn code trước, chúng ta đã dùng thẻ tự đóng cho component:

```vue-html
<MyComponent />
```

Điều này là vì trình phân tích template của Vue hiểu `/>` là dấu hiệu kết thúc bất kỳ tag nào, bất kể loại của nó.

Tuy nhiên, trong template trong DOM, chúng ta phải luôn dùng thẻ đóng tường minh:

```vue-html
<my-component></my-component>
```

Điều này là vì đặc tả HTML chỉ cho phép [một vài phần tử cụ thể](https://html.spec.whatwg.org/multipage/syntax.html#void-elements) được bỏ qua thẻ đóng, phổ biến nhất là `<input>` và `<img>`. Với tất cả các phần tử khác, nếu bỏ qua thẻ đóng, trình phân tích HTML gốc sẽ cho rằng bạn chưa kết thúc thẻ mở. Ví dụ, đoạn code sau:

```vue-html
<my-component /> <!-- we intend to close the tag here... -->
<span>hello</span>
```

sẽ được phân tích thành:

```vue-html
<my-component>
  <span>hello</span>
</my-component> <!-- but the browser will close it here. -->
```

### Hạn Chế Vị Trí Phần Tử {#element-placement-restrictions}

Một số phần tử HTML như `<ul>`, `<ol>`, `<table>` và `<select>` có hạn chế về các phần tử con được phép bên trong chúng, và một số phần tử như `<li>`, `<tr>` và `<option>` chỉ được xuất hiện bên trong một số phần tử nhất định.

Điều này sẽ gây ra vấn đề khi dùng component với các phần tử có hạn chế như vậy. Ví dụ:

```vue-html
<table>
  <blog-post-row></blog-post-row>
</table>
```

Component tùy chỉnh `<blog-post-row>` sẽ bị đưa ra ngoài như là nội dung không hợp lệ, gây ra lỗi trong kết quả render. Chúng ta có thể dùng thuộc tính đặc biệt [`is`](/api/built-in-special-attributes#is) như là cách giải quyết:

```vue-html
<table>
  <tr is="vue:blog-post-row"></tr>
</table>
```

:::tip
Khi dùng trên các phần tử HTML gốc, giá trị của `is` phải được thêm tiền tố `vue:` để được hiểu là Vue component. Điều này cần thiết để tránh nhầm lẫn với [customized built-in elements](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements-customized-builtin-example) gốc.
:::

Đó là tất cả những gì bạn cần biết về các lưu ý khi phân tích template trong DOM — và thực ra, đây cũng là phần cuối của chương _Essentials_ của Vue. Chúc mừng bạn! Vẫn còn nhiều điều để học, nhưng trước tiên, chúng tôi khuyến khích bạn hãy nghỉ ngơi và tự mình thực hành với Vue — xây dựng thứ gì đó thú vị, hoặc xem qua một số [Ví dụ](/examples/) nếu bạn chưa xem.

Khi bạn đã cảm thấy thoải mái với những kiến thức vừa tiếp thu, hãy tiếp tục với hướng dẫn để tìm hiểu sâu hơn về component.
