# HTML

## 完整示例

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>MarkSheet</title>
    <meta name="description" content="A simple HTML and CSS tutorial">
  </head>
  <body>
    <p>Hello World!</p>
  </body>
</html>
```

## 表单

```html
<form action="/signup" method="POST">
  <p>
    <label>Title</label>
    <label>
      <input type="radio" name="title" value="mr">
      Mr
    </label>
    <label>
      <input type="radio" name="title" value="mrs">
      Mrs
    </label>
    <label>
      <input type="radio" name="title" value="miss">
      Miss
    </label>
  </p>
  <p>
    <label>First name</label>
    <input type="text" value="first_name">
  </p>
  <p>
    <label>Last name</label>
    <input type="text" value="last_name">
  </p>
  <p>
    <label>Email</label>
    <input type="email" value="email">
  </p>
  <p>
    <label>Phone number</label>
    <input type="tel" value="phone">
  </p>
  <p>
    <label>Password</label>
    <input type="password" value="password">
  </p>
  <p>
    <label>Confirm your password</label>
    <input type="password" value="password_confirm">
  </p>
  <p>
    <label>Country</label>
    <select>
      <option>Canada</option>
      <option>France</option>
      <option>Germany</option>
      <option>Italy</option>
      <option>Japan</option>
      <option>Russia</option>
      <option>United Kingdom</option>
      <option>United States</option>
    </select>
  </p>
  <p>
    <label>
      <input type="checkbox" value="terms">
      I agree to the <a href="/terms">terms and conditions</a>
    </label>
  </p>
  <p>
    <button>
      Sign up
    </button>
  </p>
</form>
```

## 其他

```html
<!DOCTYPE html>
<html>
  <body>
    <p>文档类型：表示 HTML5</p>
    <p>head 标签表示附加信息</p>
    <p>段落</p>
    一般字体 <br>
    <a href="http://www.baidu.com">标签(百度)</a>
    <br>
    图片：<img src="https://placehold.it/50x50" alt="Description">
    <br>
    输入框：
    <br>
    <label for="name">Name</label>
    <input id="name" type="text" placeholder="enter your name">
    <br>
    <input type="email" placeholder="enter your email">
    <br>
    <input type="password" placeholder="enter your password">
    <br>
    <input type="number" placeholder="enter your number">
    <br>
    <input type="tel" placeholder="enter your tel">
    <br>
    <input type="time" placeholder="enter your time">
    <br>
    <textarea></textarea>
    <br>
    <label for="check">
      <input type="checkbox" name="check" id="check" checked> I agree
    </label>
    <br>
    <label>Martrial</label>
    <label>
        <input type="radio" name="status">
        Single
      </label>
      <label>
        <input type="radio" name="status">
        Married
      </label>
      <label>
        <input type="radio" name="status">
        Divorced
      </label>
      <label>
        <input type="radio" name="status">
        Widowed
      </label>
      <br>
      <select>
          <option>January</option>
          <option>February</option>
          <option>March</option>
          <option>April</option>
          <option>May</option>
          <option>June</option>
          <option>July</option>
          <option>August</option>
          <option>September</option>
          <option>October</option>
          <option>November</option>
          <option>December</option>
        </select>
    <br>
    list：
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <br>
    表格：
    <br>
    <table>
      <tr>
        <th>ID</th><th>NAME</th>
      </tr>
      <tr>
        <td>1</td><td>REN</td>
      </tr>
    </table>
    <br>
    加粗和引用:
    <p>
      Sir <strong>Alex Ferguson</strong> once said about Filipo Inzaghi:<q>"That lad must have been born offside."</q>.
    </p>

    <br>
    文章标签：
    <article>
      <h1>Famous football quotes</h1>
      <p>
        Sir <strong>Alex Ferguson</strong> once said about Filipo Inzaghi:<q>"That lad must have been born offside"</q>.
      </p>
      <p>
        When criticized by John Carew, <strong>Zlatan Ibrahimovic</strong> replied: <q>"What Carew does with a football, I can do with an orange"</q>.
      </p>
      <p>
        <strong>George Best</strong> said <q>"I spent a lot of money on booze, birds and fast cars. The rest I just squandered."</q> when asked about his lifestyle.
      </p>
    </article>

    <article>
      <h1>Main title of the page</h1>
      <h2>A subtitle</h2>
      <p>
        Something something an other stuff and some <em>emphasis</em> and even <strong>important</strong> words.
      </p>
      <p>
        Another paragraph.
      </p>
      <ul>
        <li>One</li>
        <li>Two</li>
        <li>Three</li>
      </ul>
      <blockquote>
        Once said
      </blockquote>
    </article>
    <aside>
      <h3>My latest posts</h3>
      <ul>
        <li><a href="#">One</a></li>
        <li><a href="#">One</a></li>
        <li><a href="#">One</a></li>
      </ul>
    </aside>

    <br>
    <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Instrument</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>John Lennon</td>
            <td>Rhythm Guitar</td>
          </tr>
          <tr>
            <td>Paul McCartney</td>
            <td>Bass</td>
          </tr>
          <tr>
            <td>George Harrison</td>
            <td>Lead Guitar</td>
          </tr>
          <tr>
            <td>Ringo Starr</td>
            <td>Drums</td>
          </tr>
        </tbody>
      </table>
  </body>
</html>
```