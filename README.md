### Debug Visual Studio Code
Để debug bằng vsc, cần cấu hình file launch.json trong thư mục .vscode
Sửa lại giá trị của thuộc tính _url_ thành đường dẫn tới file html

### Attribute defer
Khi load 1 trang html có chứa external css và javascript, theo logic của browser sẽ load xong và thực thi. Điều này có khả năng gây ra lỗi khi trong file javascript có preload (trường hợp để tag script trên thẻ head) của một element nào đấy trong file html mà lúc đang tải mà chưa tải hết DOM (Data object models) trong file html.

Dùng attribute `defer` của thẻ script để giải quyết vấn đề này.

Từ khóa `defer` để đánh dấu cho browser hiểu rằng, tải xong và chờ đến khi tải hết trang html thì mới thực thi code trong file javascript

### Toán tử == và ===
##### Toán tử ==
So sánh giá trị của 2 biến

##### Toán tử ===
So sánh giá trị và kiểu của 2 biến

### Toán tử so sánh giữa object và array trong js
- Array và object là kiểu **đặc biệt** trong js
    
```javascript
    const person1 = { name: 'Max' }
    const person2 = { name: 'Max' }
    person1 == person2 => false
    person1 === person2 => false
    const person3 = person1
    
    person3 ==(===) person1 => true
```

- **Lưu ý:** Điều này áp dụng cho cả mảng
- Ví dụ so sánh giữa 2 object có cùng thuộc tính như nhau { name: 'Max' }
=> Javascript sẽ luôn cho ra kết quả là false không quan tâm là === hay ==. Đơn giản là vì 2 object này không cùng **_kiểu_**.

### Toán tử && và ||
- So sánh như những ngôn ngữ lập trình khác

### Kiểu dữ liệu 'falsy' và 'truthy'
Thông qua ví dụ sau:

```javascript
const nameInput = 'Max'
if (nameInput === 'Max') {
    ...
}
```
Thông thường đối với điều kiện trong if chỉ có thể truyền vào 1 boolean expression.
Nhưng đối với js thì còn có thể dùng như sau:


```javascript
const nameInput = 'Max'
if (nameInput) {
    ...
{
```

Lúc này **nameInput** đang là kiểu string, thì js sẽ thử convert biến này bằng boolean bằng cách kiểm tra xem biến **nameInput** có empty hay không nếu cần thiết
> ##### Chú ý
> - **Nếu như có giá trị 0** => trả về false
> - **Khác 0** => trả về true
> - **Array, object** => true
> - **null**, **undefined**, **NaN** => false

### Hàm prompt()
Lấy dữ liệu nhập từ bàn phím của người dùng
```javascript
prompt('Nhập dữ liệu', '100');
```
Với tham số đầu tiên là title của cái prompt.
Tham số thứ 2 là giá trị input mặc định
Kiểu trả về là string

### Boolean tricks với toán tử logic

##### Toán tử !!
Khi so sánh 1 biến kiểu string thông thường, nếu chỉ có 1 dấu **!** thì được convert thành falsy nếu biến đó rỗng.
Nếu dùng toán tử **!!** thì sẽ ép hoàn toàn về kiểu false
```javascript
const inputName = '';
const isValid = !!inputName; //false
```

##### Toán tử ||
```javascript
const name = inputName || 'Max';
```
Dòng này đương tương với
```javascript
const name;
if (inputName) {
    name = inputName;
} else {
    name = 'Max';
}
```
_Giải thích:_ Cơ chế hoạt động của toán tử **||** sẽ trả về giá trị truthy đầu tiên mà nó kiểm tra. Nghĩa là trong phép so sánh

```javascript
inputName || 'Max'
```
Xét inputName. Nếu không rỗng => trả về giá trị true, js gắn giá trị của **inputName** vào biến **name**. Ngược lại sẽ trả về giá trị false và xét tiếp `'Max'`. Vì `'Max'` luôn trả về true nên sẽ gán `'Max'` vào biến **name**.

##### Toán tử &&
```javascript
inputName && 'Max'
```
Nếu giá trị đầu truthy thì luôn trả về giá trị thứ 2
Nếu giá trị đầu falsy thì trả về giá trị đầu luôn

### Vòng lặp for
##### For index
Duyệt qua các phần tử trong mảng thông qua index
```javascript
let arrays = [1,2,4,5,7,4,7,8,9,4,21];
for(let i = 0; i < arrays.length; i++) {
    console.log(arrays[i]);
}
```

##### For in (array)
Duyệt các phần tử trong mãng, trả về index của phần tử đó
```javascript
let arrays = [1,2,4,5,7,4,7,8,9,4,21];
for(const element in arrays) {
    console.log(element);
}
```

##### For of (object)
Duyệt các thuộc tính của object
> Hoặc

Duyệt từng phần tử trong mảng và trả về giá trị của phần tử đó
```javascript
const person = {
    id: 69,
    name: 'Huy Phùng',
    gender: true,
    age: 21,
    dob: '04/03/2000'
};
for(const prop of person) {
    console.log(`Property: ${prop}`);
    console.log(`Value of property: ${person[prop]}`);
}
```

##### Combined for loop (Mảng của nhiều object)
Duyệt mảng với phần tử là object
```javascript
let arrays = [{name: 'Max'}, {name: 'Min'}, {name: 'Med'}];
for(const element in arrays) {
    for(const prop of element) {
        console.log(`Property: ${prop}`);
        console.log(`Value of property: ${element[prop]}`);
    }
}
```

### Vòng lặp while / do - while
Giống như mọi ngôn ngữ lập trình khác

### Từ khóa var, let và const
||var  |let  |const  |
|-----|---------|---------|---------|
|Sử dụng|Khởi tạo biến|Khởi tạo biến|Khởi tạo hằng số|
|Phiên bản|Dành cho phiên bản ES5 trở về|ES6 trở lên|ES 6 trở lên|
|Phạm vi truy cập|function và global|trong khối lệnh|trong khối lệnh|

##### _Giải thích:_
- Từ khóa **var**:
    - Khai báo trong function thì là biến cục bộ.
    - Khai báo ngoài function thì là biến toàn cục.
    - Ví dụ dòng lệnh dưới đây vẫn chạy đúng
    ```javascript
    var name = 'Max';
    
    if (name === 'Max') {
        var hobbies = ['Sport', 'Cooking'];//Lúc này hobbies đang là biến toàn cục
        console.log(hobbies);    
    }

    function greet() {
        var age = 30;
        var name = 'Manuel';
        console.log(name, age, hobbies); //nên ở đây có thể truy cập được
    }
    
    console.log(name, hobbies);
    greet();
    //output không có lỗi
    ```
- Từ khóa **let** và **const**
    - Phạm vị 'scoped': chỉ tính từ phạm vi mở ngoặc nhọn mở { tới khi gặp ngoặc nhọn đóng }
    - Nghĩa là phạm vi hoạt động nằm trong khối lệnh như if, else, try, catch, vòng lặp, v.v
    ```javascript
    var name = 'Max';
    
    if (name === 'Max') { //phạm vi của biến hobbies
        let hobbies = ['Sport', 'Cooking'];//Ở đây vẫn có thể truy cập được
        console.log(hobbies);    
    } //kết thúc phạm vi của biến hobbies

    function greet() {
        var age = 30;
        var name = 'Manuel';
        console.log(name, age, hobbies); //Không thể truy cập từ đây
    }
    
    console.log(name, hobbies); //Không thể truy cập từ đây
    greet();
    //output chắc chắn lỗi vì không thấy khai báo hobbies
    ```
    - Hoặc như đoạn code bên dưới cũng lỗi
    ```javascript
    {
        let test = 'Hello, World!';
        console.log(test); //Đến đoạn này vẫn chạy được
    }
    console.log(test); //đến đây phát sinh lỗi
    ```
### Hoisting trong javascript
Ví dụ bên dưới
```javascript
console.log(userName);

var userName = 'Max';

//output: undefined
```
Và
```javascript
console.log(userName);

let userName = 'Max';

//output: Lỗi chưa khai báo biến userName
```

_Tại sao lại có thể vô lý như vậy nhỉ?_

**Giải thích**
Vì hoisting là hành động mặc định của javascript. Trong quá trình compile code, trình biên dịch của trình duyệt sẽ tự động chuyển những dòng lệnh khai báo biến hay hàm lên đầu file. Cho nên khi bắt đầu execute sẽ không bị lỗi.

**Lưu ý**
- Đối với từ khóa **var** => biên dịch bình thường.
- Đối với từ khóa **let** thì sẽ bắn ra lỗi **ReferenceError**.
- Đối với từ khóa **const** thì sẽ lỗi syntax.

### Strict mode a.k.a Chế độ nghiêm ngặt về kiểu
Ví dụ trong file _app.js_ bên dưới
```javascript
'use strict'; //thêm dòng này để bật strict mode
```

### Phân biệt vùng nhớ heap và stack
##### Vùng nhớ heap
Là nơi lưu trữ dài hạn (long term).
Mọi thành phần của chương trình đều chứa ở vùng nhớ này
_Ví dụ:_ tên biên, tên hàm.
##### Vùng nhớ stack
Là nơi lưu trữ ngắn hạn (short term).
Mọi giá trị của biến hay lời gọi hàm (call stack) đều được lưu ở đây

### Kiểu nguyên thủy (Primitive) và kiểu tham chiếu (Reference)

##### 1. Kiểu nguyên thủy
- Gồm có **string**, **number**, **boolean**, **null**, **undefined**, **symbol** (kiểu nâng cao chưa học)
- Thường được lưu ở vùng nhớ stack nếu dùng xong xóa
- Cũng có thể lưu ở heap nếu như thường xuyên dùng
- Gán vào biến khác thì sẽ sao chép giá trị chứ không trỏ vào cùng 1 ô nhớ.
```javascript
let name = 'Max';
let otherName = name; //otherName = 'Max'
name = 'Manuel';
console.log(otherName); //output: 'Max'
```

##### 2. Kiểu tham chiếu
- Tất cả cái object (vd: mảng, lớp,...)
- Được lưu ở vùng nhớ heap
- Thứ được lưu trong vùng nhớ heap không phải là *giá trị* mà là **một con trỏ được trỏ tới địa chỉ của ô nhớ chứa giá trị được lưu**
- Giả sử có 2 biến A và B, gán từ biến A vào biến B thì cả 2 đều trỏ tới cùng 1 ô nhớ. Thay đổi ở biến A => thay đỗi luôn ở biến B và ngược lại.
- Cách để copy dữ liệu vào biến B nhưng không làm thay đổi giá trị của biến A là thông qua cú pháp sau:
    ```javascript
    let person1 = { name: 'Huy Phùng', age: '21' };
    let person2 = { ...person1 }; //Sử dụng toán tử ...
    //Lúc này hệ thống tạo một con trỏ mới
    //sao chép dữ liệu đến vị trí mà con trỏ mới trỏ vào
    ```
- Đây chính là ví do vì sao toán tử === luôn trả về false đối với việc khởi tạo 2 object có cùng thuộc tính và giá trị

### Function nâng cao
- Function trong js vừa là object, vừa là thuộc tính của object (method) ...
```javascript
const person = {
  greet: function greet() {
    console.log('Hello there!');
  }
};

person.greet();
//output: Hello there!
```
Lưu function trong biến sẽ gây lỗi khi gọi function đó ở bất kỳ chỗ nào. Ví dụ:
```javascript
const start = function startGame() {
    console.log('Starting game...');
}

startGameBtn.addEventListener('click', startGame); //câu lệnh này lỗi
//Output: trình duyệt sẽ quăng ra lỗi chưa khởi tạo hàm
//Nếu muốn dùng cách này thì phải thay tham số startGame thành start (tên biến trỏ tới hàm)
```
Hoặc có thể thay bằng cách dưới, lưu 1 hàm nặc danh vào tên bên:
```javascript
const start = function() {
  console.log('Game is starting...');
}
startGameBtn.addEventListener('click', start);
```
##### Các cách khác nhau để định nghĩa 1 function
1. Khai báo function / function statements
```javascript
function multiply(a, b) {
    return a * b;
}
```
2. Dùng biểu thức hàm a.k.a function expression
```javascript
const multiply = function(a,b) {
    return a * b;
}

const divide = function(a, b) => a / b; //cái này sai
```
Lưu ý với cách 2:
- Phải khai báo trước thì mới sử dụng được. Nếu như gọi hàm trước khi khai báo thì sẽ lỗi
    ```javascript
        multiply(1, 2); // lỗi chưa initialized
        const multiply = function(a,b) {
            return a * b;
        }

        //multyply(1, 2);
    ```
##### Sử dụng lambda
> Bản chất cùa lambda là anonymous function - *trích* Giáo.làng

```javascript
// Không tham số
const sum = () => {
    //your code here
};
```
```javascript

// Một tham số

const check = isValid => {
    //your code here
};
```
```javascript
// 2 tham số

const sum = (a, b) => {
    //your code here
    //câu lệnh return là bắt buộc ở trường hợp này
};
```

```javascript
// Chỉ có 1 dòng lệnh

const sum = (a, b) => a + b;
```
### Argument mặc định trong Javascript
Trong hàm sum có 2 tham số
```javascript
const sum = (a, b) => a + b;

let result = sum(5,6); //truyền đủ tham số
result = sum(999) // truyền không đủ tham số nhưng vẫn chạy và không văng lỗi
```
Điều đặc biệt ở đây, trong các ngôn ngữ lập trình khác, 1 hàm lúc declare có bao nhiêu tham số thì phải truyền đủ bấy nhiêu. Nhưng trong javascript thì lại khác.
Mặc dù hàm **sum** có 2 tham số nhưng javascript vẫn có thể thực thi mà không văng lỗi.
**Giải thích**:
  - Khi truyền không đủ tham số, javascript sẽ tự động điền giá trị cho tham số còn lại là undefined
  - Có thể gán giá trị trước cho nó (giống optional agrument trong C#)
  - Tham số đầu tiên luôn là tham số bắt buộc nên không đổi chỗ tham số a và b được
    ```javascript
    const sum = (a, b = 10) => a + b;
    ```
### Rest Parameters hay còn gọi là rest operator
Kí tự là dấu 3 chấm ...
Ví dụ trong hàm **sumUp**
```javascript
const sumUp = (a, b, c, d) => a + b + c + d;

//hoặc

const sumUp = (numbers) => {
    let sum = 0;
    for(const num of numbers) {
        sum += num;
    }
    return sum;
};
```
2 hàm trên đều bị fix cứng tham số đầu vào. Nghĩa là hàm sumUp trên thì chỉ truyền vào được tối đa 4 phần tử. Hàm sumUp bên dưới thì lại chỉ truyền vào 1 mảng số.
=> rest operator được tạo ra để giải quyết việc truyền tham số một cách dynamically.

```javascript
const sumUp = (...numbers) => {
    let sum = 0;
    for(const num of numbers) {
        sum += num;
    }
    return sum;
};
```

Tương tự như C#
```csharp
public double sumUp(param int[] numbers) {
    double sum = 0;
    foreach(int number in numbers) {
        sum += number;    
    }
    return sum;
}
```
**Lưu ý**: 
- Các tham số khác kiểu nếu truyền sau rest parameter thì sẽ không được tính. Nên nếu có tham số khác thì luôn phải đặt trước rest parameter
- Chỉ có duy nhất 1 rest parameter được truyền vào trong 1 function

**keyword arguments (không khuyến khích)**
- Là một cách để thay thế rest operator (...)
- Chỉ có thể dùng keyword `arguments` khi có khai báo từ khóa *function*
  Ví dụ sau:
  ```javascript
  const subtractDown = function() {
      let sum = 0;
      for(const number of arguments) {
          sum -= number;
      }
      return sum;
  }
  ```
### Tạo function trong function
```javascript
const sumUp = (...numbers) => {
    const isValidNumber = (number) => {
        return isNaN(number) ? 0 : number;
    };
    let sum = 0;
    for(const num of numbers) {
        sum += isValidNumber(num);
    }
    return sum;
};

console.log(sumUp(1, 2, 3, 4, 5));
```
Phạm vi sử dụng chỉ trong function

### Hiểu về Callback function
- Đây là một hàm được gọi khi thực thi xong trong hàm khác
- Callback tức là ta truyền một đoạn code (Hàm A) này vào một đoạn code khác (Hàm B). Tới một thời điểm nào đó, Hàm A sẽ được hàm B gọi lại (callback).
```javascript
const sumUp = (resultHandler,...numbers) => {
  const isValidNumber = (number) => {
    return isNaN(number) ? 0 : number;
  };
  let sum = 0;
  for (const num of numbers) {
    sum += isValidNumber(num);
  }
  //Đây là callback function
  resultHandler(sum);
};

const showResult = (result) => {
  console.log(`The result after summaried is ${result}`);
};

sumUp(showResult, 1, 2, 'aaaa', 4, 5, 'asdf', 6);

//output
//The result after summaried is 18
```
### Phương thức bind() trong function prototype
Xem lại cho hiểu :D

# DOM
Bản chất của DOM chính là cây thư mục
Ví dụ như bên dưới:
- html
    - head
        - title
            - h1
    - body
        - div
            - p

### Truy xuất đối tượng DOM

##### Hàm querySelector(), getElementById(),...
Điểm chung của các hàm ở mục này đều là trả về 1 element duy nhất
**querySelector(selector)**
Truy xuất theo CSS selector
Ví dụ CSS selector là thẻ p. Nhưng trong 1 file html thì có rất nhiều thẻ p => Trả về đối tượng p được tìm thấy đầu tiên trong file

**getElementById(id)**
Truy xuất theo id của element

**Lưu ý:**
Bản chất của các node DOM (các element) cũng chỉ là object => giá trị tham chiếu (reference value) nên cả 2 method trên đều trả về địa chỉ chứ không phải giá trị.

##### Hàm querySelectorAll(), getElementsByTagName(),...

##### querySelectorAll() và getElementsByTagName()
Trả về dánh sách tập hợp của các elements (array-like). Ví dụ NodeList. Có thể support các hàm của array hoặc không
Có nhiều cách để truy xuất như truy xuất bằng CSS selector, bằng tag name hoặc bằng CSS class.

##### Phân biệt giữa nodes và elements
**Nodes**
- Là các objects tạo nên DOM
- Tất cả mọi thứ trong DOM đều là nodes
- Các *thẻ html* được xem là **element nodes**
- Còn *text* sẽ tạo ra các **text nodes**
- *Thuộc tính* (attributes) sẽ tạo ra các **attribute node**

**Elements**
- Là một kiểu của nodes
- Là node được tạo ra bởi một thẻ html đã được render, không phải nội dung văn bản bên trong thẻ đó
- Điểm khác biệt ở đây là element sẽ có các thuộc tính và properties để tương tác
    - Ví dụ như thêm xóa element, thay đổi style, nội dung,...
- Bên node cũng có các method này nhưng không thường xuyên sử dụng như của element
- Elements có thể được chọn bằng nhiều cách (thông qua javascript)

**Hướng dẫn sử dụng getElementById**
Đây là phương thức chỉ có đối tượng document có thể sử dụng

Từ các element (h1, h2, p, ul, li, ...) trở xuống thì sử dụng querySelector để truy xuất tới các element con.

**Hướng dẫn sử dụng querySelector**
Phương thức của element.
Truyền vào 1 tham số kiểu chuỗi. Tham số này sẽ là 1 lớp ccc (.list-item,...)
```javascript
const ul = document.getElementById('list');
ul.querySelector('.list-item');
//output
//<li class="list-item">Item 2</li>
```
Nếu muốn chọn hết thì sử dụng hàm *querySelectorAll* (đối tượng document hay element đều sử dụng được)

Ví dụ:
- Chọn ul li:first-of-type
```javascript
document.querySelector('ul li:first-of-type');
//output: <li>Item 1</li>

//hoặc

document.querySelector('ul li:first-of-type');
//output: <li class="list-item">Item 3</li>
```
### Phân biệt attributes (thuộc tính) và properties (thuộc tính)
Thông thường, các attributes được map tới các properties và "**live synchronization**" được set up
Ví dụ trong 1 element input phía dưới:
```html
<input id="input-1" class="input-default" value="Enter text...">
```
*Attributes:* id, class, value... (nằm trong html code, trên thẻ)

```javascript
const input = document.getElementById('input-1');
input.id... //đây là các properties
input.className...
input.value...
```
*Properties:* id, className, value,... (luôn được tự động thêm vào khi các object element được khởi tạo)

Mối quan hệ mapping 1-1 giữa 1 attribute và 1 property, **Có live-synchronize**
Ví dụ:
> Attribute **id** map tới property **id**
Attribute **value** map tới property **value**

Mối quan hệ mapping 1-N
Ví dụ:
> property **className** trả về 1 array-like object

### Duyệt DOM
##### Khái niệm child, descendant, parent, ancestor

**Child**
Là thẻ thấp hơn thẻ cha 1 cấp. 
Direct child or element
Ví dụ:
```html
<div>
  <p>A <em>test!</em></p>
</div>
```
Thẻ p là con của div, còn thẻ em thì không phải là con của div

**Descendant**
Là những thẻ con nằm trong thẻ cha
Direct or indirect child note or element
Ví dụ:
```html
<div>
  <p>A <em>test!</em></p>
</div>
```
Thẻ p và em là descendant của div

**Parent** và **Ancestors**
Hai khái niệm này giống đối lập với *child* và *descendant*
Parent - Child
Ancestor - Descendant
Sibling là anh em bằng cấp

### Vận dụng DOM vào styling

**Thông qua thuộc tính *style***
- Trực tiếp target tới một thành phần CSS trong element đó
- Điều khiển style theo dạng inline.
- Các thuộc tính con nằm trong thuộc tính *style* đều có cùng tên với các thuộc tính CSS và được viết theo format camelCase.
    - Ví dụ: background-color thành backgroundColor

**Thông qua className**
- Set trực tiếp các lớp CSS được assigned trong element
- Set/ điều khiển tất cả các class trong 1 lần
- Cũng có thể điều khiển id hoặc các properties khác
```javascript
const section = document.querySelector('section');

section.className = '';

//lúc này attribute class của thẻ section sẽ là 1 chuỗi rỗng
//Có thể dùng thuộc tính className để assign những lớp của bootstrap
```
**Thông qua classList**
- Thêm xóa sửa các lớp CSS của 1 element
- Có thể dùng với className


**Thêm element thông qua HTML trong code**
Có thể dùng cách cách dưới
```javascript
const ul = document.querySelector('ul');

//Cập nhật lại các thành phần bên trong ul
ul.innerHTML += '<p>new element</p>'; 
```
Cách trên có thể dễ hiểu vì nó sẽ cập nhật lại toàn bộ bên trong 1 element cha. Nhưng sẽ làm chậm hệ thống vì mỗi lần cập nhật là mỗi lần tải lại và chứng minh rằng không có học về UX/UI :). Ngoài ra còn có thể gây lỗi nếu như có thể input bên trong.
- **Giải thích**: vì khi người dùng nhập vào input, và mình toggle để render lại thuộc tính innerHTML thì input của người dùng sẽ mất vì thẻ đó đã được render lại.

*Một cách khác tốt hơn để thêm element*
- Sử dụng hàm **insertAdjacentHTML(position, text)**.

Trong cách này, position là một tham số đã được định nghĩa sẵn, google để biết thêm chi tiết.
- Tham số *position*
    - `'beforebegin'`: ở trước của element gọi hàm
    - `'afterbegin'`: bên trong element và đằng trước first child
    - `'beforeend'`: bên trong element và ở sau last child
    - `'afterend'`: ở sau element gọi hàm
    ```html
    <!-- beforebegin -->
    <p>
        <!-- afterbegin -->
        foo
        <!-- beforeend -->
    </p>
    <!-- afterend -->
    ```
*Khuyến khích sử dụng cách trên vì hàm insertAdjacentHTML được hỗ trợ trên mọi trình duyệt*
**Thêm element thông qua hàm createElement(element)**
Luôn gọi hàm này bằng đối tượng document
```javascript
const list = document.querySelector('ul');

const newLi = document.createElement('li');
//newLi: <li></li>
newLi.textContent = 'Hello, World';
//newLi: <li>Hello, World</li>

list.appendChild(newLi);
//trong thẻ ul đã được thêm vào 1 node mới


```

# Iterables == Enumrable
### Iterable là gì?
**Về mặt technical**
Là các object implement giao thức "iterable" và có một method là @@iterator (Vd: symbol.iterator)
**Về mặt đỉnh nghĩa để hiểu (về mặt logic)**
Là các object có thể sử dụng vòng lặp *for-of*

*Lưu ý*: không phải iterable nào trong js cũng là array (như là Node list, String, Map, Set)

### Đối tượng Array-Like là gì?
**Về mặt technical**
Là đối tượng có thuộc tính length và sử dụng index (chỉ mục) để truy cập các item được chứa trong đó.
Về mặt định nghĩa thì như technical.

### Cách tạo một Array
Có nhiều cách tạo 1 một array
Ví dụ như bên dưới
```javascript
const arr = [1]; //tạo array với item đầu tiên mang giá trị = 1

const arr = Array(1)
const arr = Array(1, 3) //khởi tạo array và thêm 2 phần tử là 1 và 3 vào array
const arr = new Array(1) //tạo array với độ dài là 1
const arr = Array.of(1) //bad performance nếu hoạt động với số lượng phần tử lớn
const arr = Array.from([1, 2, 3]) //khuyến khích sử dụng như []
```
Có new hay không đều như nhau

**Lưu ý** về Array.**from()**
Đây là hàm dùng để convert iterable hay array-like object thành array
Tham số truyền vào là một iterable hay array-like object
Ví dụ:
```javascript
const arr = Array.from('Hello, World!');
console.log(arr);
//output:
{13} ['H', 'e', 'l', 'l', 'o', ',', ' ', 'W', 'o', 'r', 'l', 'd', '!']
```

```javascript
//Ví dụ iterable NodeList
const listItems = document.querySelectorAll('li'); 
console.log(listItems);//NodeList

const arrayListItems = Array.from(listItems);
console.log(arrayListItems); //array
```
### Những loại dữ liệu có thể lưu trong array
Lưu cùng 1 loại hoặc có thể lưu nhiều loại trong 1 array (fixed or flexible).
Phần tử đầu tiên luôn bắt đầu với chỉ mục là 0
```javascript
const hobbies = ['Cooking', 'Sports'];

const personalData = [30, 'Max', {moreDetail: []}];

const analyticsData = [[1,4], [2,5]];
```

### Cách phương thức trong array
**push(parameter) return number**
Là phương thức được cấp sẵn cho array, có chức năng **thêm 1 phần tử cuối mảng** và *trả về độ dài mới của mảng*
```javascript
const hobbies = ['Sports', 'Cooking'];
hobbies.push('Reading'); //Thêm vào cuối mảng
console.log(hobbies);

//'Sports', 'Cooking', 'Reading'
```
**unshift(parameter) return number**
Giống như *push()* nhưng **thêm phần tử vào đầu mảng**
```javascript
const hobbies = ['Sports', 'Cooking'];
hobbies.unshift('Reading'); //thêm vào đầu mảng
console.log(hobbies);

//Reading, Sports, Cooking
```

**pop() return string**
Là phương thức được cấp sẵn cho array, có chức năng **xóa một phần tử ở cuối mảng** và *trả về phần tử đó*
```javascript
const hobbies = ['Sports', 'Cooking', 'Reading'];
hobbies.pop(); //xóa phần tử ở cuối mảng
console.log(hobbies);
```

**shift() return string**
Giống như pop nhưng **xóa phần tử đầu tiên trong mảngx**

**Lưu ý:** Có thể thay đổi giá trị trong mảng nhưng không thể thay đổi biến lưu mảng đó khi sử dụng keyword khai báo const

```javascript
const arr = ['Coding', 'Sports', 'Reading'];
arr[1] = 'Dancing'; //allow
arr = ['Smiling', 'Well done']; //error

//Nếu lưu ngoài độ dài của mảng
arr[5] = 'Yolo';
//output: length = 6, empty x2 tại vì ở index 3 và 4 đang trống
```

### Phương thức splice() và slice()
Chỉ có array chính thống mới có phương thức này
Còn những kiểu con của iterable hay array-like object thì không.

**splice(start: number, deleteCount?: number, ...items)**
Kết quả trả về là *string[]*
*Bản chất:* là lấy những phần tử con nằm trong điều kiện tham số truyền vào, copy sang mảng mới và xóa đi ở mảng cũ

Tham số start: number
- Bắt đầu từ số 0 như index của mảng
- Nếu truyền vào số âm thì bắt đầu tính từ cuối mảng đi về đầu mảng

Tham số deleteCount?: number
- Số lượng phần tử cần xóa

Tham số ...items
- 1 mảng các phần tử thay thế cho các phần tử đã xóa khỏi mảng

Ví dụ 1
```javascript
const hobbies = ['Sports', 'Cooking', 'Reading'];
console.log(hobbies);
const arr = hobbies.splice();
console.log(arr); //[] trống
//--------------------------------------------
```

Ví dụ 2
```javascript
const hobbies = ['Sports', 'Cooking', 'Reading'];
//xóa những phần tử bắt đầu từ vị trí 1 trở đi
const arr = hobbies.splice(1); 
console.log(hobbies); //Sports
console.log(arr); //Cooking, Reading
```

Ví dụ 3
```javascript
const hobbies = ['Sports', 'Cooking', 'Reading'];
//Lúc này sẽ thành là chèn phần tử google vào vị trí 1
const arr = hobbies.splice(1, 0, 'Google'); 
console.log(hobbies); //['Sports', 'Google','Cooking', 'Reading']
console.log(arr); //Trống
```

Ví dụ 4
```javascript
const hobbies = ['Sports', 'Cooking', 'Reading'];
//Lúc này sẽ thực hiện 2 thao tác
//ở mảng hobbies xóa phần tử bắt đầu từ 1
//số lượng 2 phần tử và chèn vào phần tử google
//vào vị trí bắt đầu xóa (1)
//Sau đó các phần tử đã bị xóa sẽ copy sang mảng arr
const arr = hobbies.splice(1, 2, 'Google'); 
console.log(hobbies); //['Sports', 'Google']
console.log(arr); //'Cooking', 'Reading'
```
**slice(start?: number, end?: number)**
Hơi khác với phương thức *splice()* là hàm này chỉ copy chứ không xóa
Ví dụ 1
```javascript
const results = [5, 1, 8, 42, 3, -12, 115, -53, 53, 35, -12];
const arr = results.slice();
//copy toàn bộ phần tử sang 1 mảng mới
console.log(results);
console.log(arr);
```

Ví dụ 2
```javascript
const results = [5, 1, 8, 42, 3, -12, 115, -53, 53, 35, -12];
const arr = results.slice(1, 4);
console.log(results);
console.log(arr); //1, 8, 42
```

Ví dụ 3
```javascript
const results = [5, 1, 8, 42, 3, -12, 115, -53, 53, 35, -12];
const arr = results.slice(1); //bắt đầu từ vị trí số 1
console.log(results);
console.log(arr); //1, 8, 42, 3, -12, 115, -53...
```
### Phương thức concat()
Phương thức dùng để cộng 2 phần tử của 2 array khác nhau, không có tác dụng trên 2 mảng cộng lại với nahu mà sẽ trả về một mảng hoàn toàn mới
Ví dụ
```javascript
const hobbies = ['Sports', 'Reading', 'Hello'];
const hobbies2 = ['Dancing', 'Rapping', 'Tripping'];
hobbies.concat(hobbies2);
console.log(hobbies); //như cũ

const results = hobbies.concat(hobbies2);
console.log(results); //1 array mới

const result2 = hobbies.push(hobbies2);
console.log(result2);
console.log(hobbies); //lúc này phần tử cuối cùng là array chứ không phải number
```
Phương thức concat() sẽ lấy các phần tử TRONG mảng rồi thêm vào cuối của mảng gọi phương thức và trả về một mảng hoàn toàn mới (thành phần của mảng cũ được giữ nguyên)

Còn push() sẽ đẩy cả array vào thành 1 phần tử của mảng

### Phương thức forEach() của mảng
Tham số truyền vào là một anonymous function với 3 tham số như sau:
```javascript
const prices = [1.6, 5.55, 84.64, 100.44];
const tax = 0.6;
const adjustTaxArray = [];
prices.forEach((price, index, otherPrices) => {
  const adjustTaxPrice = price * (1 + tax);
  const priceObj = {index: index, adjustTax: adjustTaxPrice};
  adjustTaxArray.push(priceObj);
  otherPrices.push(adjustTaxPrice);
  console.log(otherPrices);
});
console.log(adjustTaxArray);
```

Tham số price chính là tham số iterator, tượng trưng cho 1 phần tử nằm trong mảng
Tham số index là chỉ mục của phần tử đó nằm trong mảng
otherPrices chính là mảng gọi phương thức, cũng có nghĩa 
```javascript
otherPrices = prices
```

# Browser APIs

**Làm việc với dataset a.k.a *data-\** attributes**
Tác dụng của dataset: Dùng để gán/lấy dữ liệu vào element trong DOM

Ví dụ đơn giản bên dưới:
```HTML
<div
    id="p1"
    data-extra-info="Got lifetime access, Hello World!"
>
<h2>Finish the course</h2>
<p>Finish the course within next two weeks.</p>
<button>More info</button>
</div>
```


Attribute `data-extra-info` là attribute do dev tạo, có thể tạo bất kì hay bao nhiêu attribute bắt đầu bằng tiền tố *data-* đều được. Vấn đề đặt ra bây giờ là làm thế nào JS lại có thể lấy được dữ liệu từ trong thẻ div có id là p1?
- Giải thích: Về bản chất lưu trữ, các dữ liệu của thuộc tính `dataset` đều được lưu trong DOM. Do đó lúc này thuộc tính `dataset` sẽ tự động phát sinh ra thuộc tính con `extraInfo` (viết theo camelCase), suy ra để lấy/gán dữ liệu chỉ cần thực hiện như đoạn code bên dưới
    ```javascript
    //Lấy element lưu data
    const divEl = document.getElementById('p1');

    //Lấy dữ liệu từ thuộc tính
    const info = divEl.dataset.extraInfo;
    
    //câu lệnh dưới sẽ khởi tạo 1 attribute của div trong DOM 
    //có tên là data-something-new
    divEl.dataset.somethingNew = 'Tạo mới thuộc tính somethingNew';

    
    console.log(info);
    ```
Còn tiếp... (nan3 qua1 nen hoc cai khac1 :'( )

### Bắt sự kiện (Events)

**Sự khác biệt giữa bắt sự kiện của Nodejs và trình duyệt web**
- Nodejs
Sử dụng phương thức *on()*

- Trình duyệt web
Sử dụng phương thức *addEventListener()*

Ví dụ về cách sử dụng
```javascript
//js thuần
element.addEventListener('...', event => {});

//nodejs
element.on('...', event => {});

```

**Event là 1 lớp đặc biệt trong js**
Event (lớp cha), được kế thừa từ các MouseEvent, DragEvent, ClickEvent,... . Đặc điểm chung là đều có Event Target (element được tác động đến từ phía người dùng)

**Có 2 cách để add event (1 cách cũ, 1 cách mới)**
*Cách cũ*
Sử dụng attribute của thẻ trong html
```html
<button onclick='alert("You just clicked me");'>
    Click me
</button>
```
*Cách mới*
Sử dụng javascript để bắt sự kiện
```javascript
const button = document.querySelector('button');

// Khai báo 1 anonymous function
// button.onclick = function() {

// };


const buttonClickHandler = () => {
  alert('Button was clicked!');
};

const anotherButtonClickHandler = () => {
  console.log('This was clicked!');
};

button.onclick = buttonClickHandler;
button.onclick = anotherButtonClickHandler; //override

//output This was clicked!
```
**Lưu ý** khi dùng cách mới, nên dùng phương thức addEventListener thay vì dùng properties như trong ví dụ. Vì sao lại như vậy? => Vì thuộc tính onclick bị override lại khi được gán nhiều hàm xử lí trở lên. Cho nên để tránh tình trạng này thì nên sử dụng phương thức `addEventListener()`. Còn nữa có thể dùng `removeEventListener()` để dễ dàng kiểm soát hơn

```javascript
//Lưu lại địa chỉ của hàm thực thi
const buttonClickHandler = () => {
  alert('Button was clicked!');
};

button.addEventListener('click', buttonClickHandler);

setTimeout(() => {
  //Tham số nên giống với lúc add để js biết đường mà xóa
  button.removeEventListener('click', buttonClickHandler);
  
}, 2000); //sau 2s sẽ xóa event click
```
**Lưu ý:** Không nên dùng hàm anonymous hay `function.bind(this)`. Vì mỗi khi element bị triggered sẽ tạo ra 1 function object hoàn toàn mới, nhìn code có vẻ giống nhau nhưng bản chất ở tầng logic thì lại là 2 địa chỉ khác nhau. Nếu muốn sử dụng hàm anonymous hay `function.bind()` thì phải khởi tạo 1 biến hằng để lưu địa chỉ.

**Ngoài ra** nếu tham số là `event` được truyền vào trong function thì sẽ xem được metadata của event được triggered.
```javascript
const buttonClickHandler = event => {
    console.log(event);
};

button.addEventListener('click', buttonClickHandler);

//Khi button được click sẽ hiện ra console metadata của event
```

Ví dụ:
```javascript

//Thêm hàm bắt sự kiện cho button
const buttonClickHandler = event => {
    event.target.disabled = true;
    console.log(event);
};

//Tìm tất cả button có trong DOM
const buttons = document.querySelectorAll('button');

buttons.forEach(btn => {
    btn.addEventListener('click', buttonClickHandler);
});
```
Giải thích: Trong object `event` có nhiều thuộc tính vv, và đặc biệt là thuộc tính `target` (đây chính là element được triggerd). Mà đã là element thì chắc chắn sẽ truy cập được những thuộc tính của element, ví dụ trên chính là truy xuất đến thuộc tính `disabled` của element `button`. Khi set thuộc tính `disabled = true` thì element được triggered sẽ tự động thêm attribute disabled

Tương tự như thế, javascript hỗ trợ sẵn phần lớn event tương tác với DOM. Tuỳ theo mình khai báo như thế nào như bên dưới
```javascript
//bắt sự kiện click
element.addEventListener('click', ...);

//bắt sự kiện di chuột vào element
element.addEventListener('mouseenter', ...);

//bắt sự kiện scroll của window
window.addEventListener('scroll', ...);
```

Thông tin chi tiết thì search google theo từ khoá: **Javascript Event MDN** (official)


**Ý tưởng về infinity scroll**
```javascript
let curElementNumber = 0;

function scrollHandler() {
  const distanceToBottom = document.body.getBoundingClientRect().bottom;

  if (distanceToBottom < document.documentElement.clientHeight + 150) {
    const newDataElement = document.createElement('div');
    curElementNumber++;
    newDataElement.innerHTML = `<p>Element ${curElementNumber}</p>`;
    document.body.append(newDataElement);
  }
}

window.addEventListener('scroll', scrollHandler);
```