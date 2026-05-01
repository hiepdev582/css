# CSS

## CSS basic

### I. How browsers load websites

1. Web đọc file HTML và gen ra **DOM Tree** (Document Object Model) bao gồm: Element + Attribute + Text
2. Web đọc file CSS và gen ra **Render Tree** bao gồm: DOM Tree + Style
3. **Layout** và **Painting**
4. Xử lý **JavaScript**

### II. Attribute selectors

1. `[title]`: Có attribute title
2. `[title="a"]`: Có attribute title bằng a
3. `[title^="a"]`: Có attribute title bắt đầu bằng a
4. `[title$="a"]`: Có attribute title kết thúc bằng a
5. `[title*="a"]`: Có attribute title chứa a
6. `[title~="a"]`: Có attribute title chứa a (space-separated)
7. `[title|="a"]`: Có attribute title chứa a (begins with value immediately followed by a hyphen)

### III. Font styles

1. `text-indent`: Thụt đầu dòng cho dòng đầu tiên của đoạn văn
2. `white-space`: Quyết định cách xử lý dấu cách và xuống dòng trong code (normal, nowrap, pre, pre-wrap, pre-line)
3. `text-overflow`: Khi chữ bị tràn khung, bạn muốn nó biến mất hay hiện dấu ba chấm _(Thường dùng kèm với `overflow: hidden` và `white-space: nowrap`)_
4. `word-break`: Quyết định có được phép ngắt ngang một từ hay không
5. `overflow-wrap`: Cho phép trình duyệt ngắt dòng ở giữa một từ "không thể ngắt" để ngăn việc văn bản tràn ra ngoài khung chứa
6. `hyphens`: Tự động thêm dấu gạch nối (-) khi ngắt từ ở cuối dòng
7. `@font-face`: WOFF / WOFF2 (Web Open Font Format): Định dạng tốt nhất hiện nay, được nén tốt và hỗ trợ rộng rãi. WOFF2 là tiêu chuẩn vàng vì dung lượng cực nhẹ
   - `font-display: swap;`: Hiển thị font chữ mặc định ngay lập tức, sau đó thay thế bằng font đã load
   - Ưu tiên định dạng WOFF2 và sử dụng Preload:

   ```html
   <link
     rel="preload"
     href="/fonts/myfont.woff2"
     as="font"
     type="font/woff2"
     crossorigin
   />
   ```

   - Font Subsetting (Cắt tỉa phông chữ)

   ```css
   @font-face {
     font-family: "MyCustomFont";
     src: url("fonts/vietnam-subset.woff2") format("woff2");
     unicode-range:
       U+0102-0103, U+0110-0111, U+1EA0-1EF9; /* Chỉ dải ký tự tiếng Việt */
   }
   ```

   - Sử dụng Variable Fonts (Phông chữ biến đổi): Thay vì tải 4 file cho: Regular, Medium, Bold, Italic, chỉ cần tải duy nhất 1 file Variable Font. Điều chỉnh độ đậm (weight) và độ nghiêng một cách linh hoạt bằng CSS

   ```css
   @font-face {
     font-family: "RobotoFlex";
     src: url("fonts/RobotoFlex-Variable.woff2") format("woff2-variations");
     font-weight: 100 900;
   }
   ```

### IV. Layout

1. **Grid (Bố cục 2 chiều)**: Dùng Grid khi muốn xây dựng khung xương (layout) cho toàn bộ trang web (Header, Sidebar, Main, Footer)
   - `grid-template-columns: repeat(3, 1fr) / minmax(200px, 1fr) 1fr 1fr / repeat(auto-fit, minmax(250px, 1fr))`
   - `grid-template-rows: repeat(3, 1fr)`
   - `grid-auto-columns: 100px`: Quy định chiều cao mặc định cho các cột không được định nghĩa trong `grid-template-columns`
   - `grid-auto-rows: 100px`: Quy định chiều cao mặc định cho các hàng không được định nghĩa trong `grid-template-rows`
   - `grid-column`: Chỉ định phần tử sẽ chiếm bao nhiêu cột và ở vị trí nào
   - `grid-row`: Chỉ định phần tử sẽ chiếm bao nhiêu hàng và ở vị trí nào
   - `grid-template-areas` & `grid-area`: Định nghĩa khu vực cho từng phần tử
2. **Flexbox (Bố cục 1 chiều)**: Dùng Flexbox khi chỉ quan tâm đến việc sắp xếp các phần tử theo 1 hàng hoặc 1 cột
   - `flex`: `flex-grow` + `flex-shrink` + `flex-basis`
   - `flex-flow`: `flex-direction` + `flex-wrap`
   - `order`: Thay đổi thứ tự xuất hiện của các phần tử
3. **Multi-column**: Dùng khi có 1 khối văn bản dài và muốn nó tự động chảy qua các cột như báo giấy

- `columns`: `column-count` + `column-width`
- `column-gap`: Khoảng cách giữa các cột
- `column-rule`: Đường viền ngăn cách giữa các cột
- `column-span`: `all` - Cho phép 1 phần tử _(thường là tiêu đề)_ ngắt ngang các cột và trải dài ra toàn bộ chiều rộng
- `column-fill`: `balance` _(mặc định, làm cho các cột có chiều cao bằng nhau)_ / `auto` _(lấp đầy cột đầu tiên trước rồi mới sang cột tiếp theo)_

4. **Float**: Cho chữ bao quanh 1 hình ảnh. Đây là mục đích nguyên bản của thuộc tính này
   - Thuộc tính `clear` có tác dụng loại bỏ sự ảnh hưởng của Float. Nó ra lệnh cho phần tử đứng sau đó phải "nhảy" xuống dưới phần tử bị float.
   - `display: flow-root`: Là 1 cách hiện đại để "reset" Float mà không cần dùng Clearfix. Nó tạo ra một Block mới "chịu trách nhiệm" chứa toàn bộ chiều cao của các thành phần con bên trong nó, qua đó kéo container tự động bao quanh các phần tử con đã bị float.

5. **Table**: Dùng khi muốn tạo 1 danh sách hoặc cấu trúc dạng bảng mà các cột phải có chiều cao bằng nhau và căn lề dọc chuẩn xác

- `display: table`
- `display: table-row`
- `display: table-cell`

6. **Position**
   - `static`: Mặc định. Phần tử đứng yên tại vị trí của nó
   - `relative`: Tương đối so với vị trí ban đầu của nó, không làm ảnh hưởng đến vị trí của các phần tử xung quanh
   - `absolute`: Tuyệt đối so với phần tử cha gần nhất có `position: relative` hoặc `absolute`. Nếu không có thì sẽ so với viewport
   - `fixed`: Cố định so với viewport
   - `sticky`: Kết hợp giữa `relative` và `fixed`. Phần tử sẽ di chuyển như `relative` cho đến khi đạt đến một ngưỡng nhất định, sau đó sẽ dính chặt vào viewport như `fixed`

### V. Background

**Shorthand**: background: red url(./image.jpg) 10px 10px repeat-x fixed;

1. `background-color`: red
2. `background-image`: url(./image.jpg)
3. `background-position`: 10px 10px
4. `background-repeat`: repeat-x
5. `background-attachment`: fixed

### VI. List style

- `list-style-position`: inside / outside

### VII. Box model

1. Inline: width, height, margin và padding top / bottom không có tác dụng

### VIII. CSS filter

1.  `filter`: drop-shadow(5px 5px 1px rgb(0 0 0 / 70%))

### IX. Writing mode

- `horizontal-tb`: Traditional top-to-bottom, left-to-right horizontal writing.
- `sideways-rl`: Vertical writing, top-to-bottom lines, right-to-left columns.
- `sideways-lr`: Vertical writing, top-to-bottom lines, left-to-right columns.

### X. CSS Shapes

1.  `shape-outside`: circle() / polygon()
2.  `shape-margin`
3.  `clip-path`: polygon()

    ```css
    .shape-circle {
      /* 1. BẮT BUỘC: Phải dùng float */
      float: left;

      /* 2. BẮT BUỘC: Phải có kích thước */
      width: 200px;
      height: 200px;

      /* Làm cho hình ảnh trông đẹp hơn (bo góc tròn) */
      border-radius: 50%;
      object-fit: cover;

      /* 3. QUAN TRỌNG: Định nghĩa hình dạng cho chữ bao quanh */
      /* circle(bán_kính at tâm_x tâm_y) */
      shape-outside: circle(50% at center);

      /* Tạo khoảng cách giữa chữ và hình */
      shape-margin: 20px;

      /* Các thuộc tính trang trí khác */
      margin-right: 10px; /* Margin thông thường để đẩy chữ nếu Shapes không hỗ trợ */
      border: 5px solid #eaeaea;
    }
    ```

### XI. Background Image text

```css
p {
  color: white;
  display: inline-block;
  background: url("./image.jpg") no-repeat center;
}

.text-clip {
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
```

---

## CSS Advance

### I. CSS Methodologies

1. **BEM**: Block\_\_Element--Modifier
2. **SMACSS**: Scalable and Modular Architecture for CSS

   ```css
   @import "base.css";
   @import "layout.css";
   @import "module.css";
   @import "state.css";
   @import "theme.css";
   ```

### II. Cascade Layers

- `@layer`
- Theo đặc tả của CSS, thứ tự lớp được quyết định bởi lần đầu tiên chúng được nhắc tới nên phải đặt thứ tự @layer ở đầu file.

  ```css
  @layer layer2, layer1;

  @import url(./layer1.css) layer(layer1);
  @import url(./layer2.css) layer(layer2);
  ```

---

## CSS Optimization

### I. Responsive

1. Luôn dùng relative unit (element, font,...)
2. `clamp(MIN, VAL, MAX)`
3. Web safe fonts

- **sans-serif** (_Hiện đại, dễ đọc trên màn hình kỹ thuật số_): Arial, Helvetica, sans-serif

- **monospace** (_Tiêu chuẩn để viết code vì dễ dàng căn lề và phát hiện lỗi_): Courier New, Courier, monospace

- **serif** (_Trang trọng, truyền thống, thường được dùng cho các văn bản in ấn_): Times New Roman, Times, serif

- **cursive** (_Mô phỏng theo nét chữ viết tay, nghệ thuật_)

- **fantasy** (_Phá cách, sáng tạo, độc lạ_)
