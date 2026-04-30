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

### III. Background

**Shorthand**: background: red url(./image.jpg) 10px 10px repeat-x fixed;

1. `background-color`: red
2. `background-image`: url(./image.jpg)
3. `background-position`: 10px 10px
4. `background-repeat`: repeat-x
5. `background-attachment`: fixed

### IV. Box model

1. Inline: width, height, margin và padding top / bottom không có tác dụng

### V. Grid

1. `grid-template-columns`
2. `grid-template-rows`

### VI. CSS filter

1.  `filter`: drop-shadow(5px 5px 1px rgb(0 0 0 / 70%))

### VII. Writing mode

- `horizontal-tb`: Traditional top-to-bottom, left-to-right horizontal writing.
- `sideways-rl`: Vertical writing, top-to-bottom lines, right-to-left columns.
- `sideways-lr`: Vertical writing, top-to-bottom lines, left-to-right columns.

### VIII. CSS Shapes

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

### IX. Background Image text

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
