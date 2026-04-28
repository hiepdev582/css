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
