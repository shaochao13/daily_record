
# Types

Solidity is a statically language.

## Value Types

### Booleans

### Integers

`uint`默认为`uint256` 它的取值范围为：0 ～ 2**256-1。
`int`默认为`int256` 它的聚会范围为：-2**255 ~ 2**255 -1。

### Address
它是一个16进制数字。

### bytes


## Reference Types

### Struct

```solidity {.line-numbers}
struct Car{
    string model;
    uint year;
    address owner;
}

Car public car;
Car[] public cars;
mapping(address => Car[]) public carsByOwner;

function examples() external {
    Car memory toyota = Car("Toyota", 1990, msg.sender);
    Car memory lambo = Car({year: 1980, model: "Lamborghini", owner: msg.sender});
    Car memory tesla;
    tesla.model = "Tesla";
    tesla.year = 2010;
    tesla.owner = msg.sender;

    cars.push(toyota);
    cars.push(lambo);
    cars.push(tesla);

    cars.push(Car("Ferrari", 2020, msg.sender));

    //使用memory 定义在内在中的变量，修改是无效的，
    Car memory _car = cars[0];
    // 此处的修改不会生效
    _car.year = 1991;

    // 使用storage定义在存储中的变量，即读取了状态变量，则可以进行修改数据了
    Car storage _car2 = cars[0];
    // 此处才能修改
    _car2.year = 1992;

    // delete 不会将元素从数组中或者变量中删除，只会将其用元素的数据类型的默认值进行替换
    delete cars[1];
}
```

### Enum
```solidity {.line-numbers}
enum Status {
    None,
    Pending,
    Shipped,
    Completed,
    Rejected,
    Canceled
}

Status public status; 

function get() external view returns (Status) {
    return status;
}

function set(Status _status) external {
    status = _status;
}

function ship() external {
    status = Status.Shipped; 
}

// 重置枚举为默认值，即为此枚举的第一个值
function reset() external {
    delete status;
}
```
### Array

动态数组只能用在状态变量中，局部变量只能是定长数组。

```solidity {.line-numbers}
//动态数组
uint[] public nums = [1,2,3];
//定长数组
uint[3] public numsFixed = [4,5,6]; 

function examples() external {
    //往数组未尾添加元素
    nums.push(4); // [1,2,3,4]

    // delete 不会减少数组的元素个数，只是将指定位置的元素值变为“0”
    delete nums[1]; // [1,0,3,4]
    // 可以用在定长数组上，因为它不会改变数据的长度
    delete numsFixed[1];

    // 从数组的未尾删除一个元素，会改变数组的长度。
    nums.pop(); // [1,0,3]

    // 在内存中定义数组
    // 在内存中定义数组时，只能定义定长的数组
    uint[] memory a_list = new uint[](5);
    delete a_list[2];
    a_list[1] = 10;
}

// 返回数组
function returnArray() external view returns (uint[] memory) {
    return nums;
}
```

### 删除数组指定位置的元素
```solidity {.line-numbers}
uint[] public arrs = [1,2,3,4,5];

// 删除数组指定位置的元素
// 这种方法比较消耗 GAS费
function remove(uint _index) public lessThanArrLingth(_index) {
    //如要删除 arrs 数组的第2个元素,即arrs[1]
    //执行过程： [1,2,3,4,5] -->将要_index后面的元素的值都往前“移”一位 --> [1,3,4,5,5] ---> 执行pop()，将最后的元素pop掉 --> [1,3,4,5]
    for(uint i = _index; i < arrs.length - 1; i++){
        arrs[i] = arrs[i + 1];
    }
    //删除掉数组最后一个元素
    arrs.pop();
}

// 删除数组指定位置的元素
// 这种方法消耗的GAS费，相对上面的方法会少一些
// 但这种方法会打乱数组的排序
function remove2(uint _index) public lessThanArrLingth(_index) { 
    //执行过程： [1,2,3,4,5] -->remove2(1)用最后一个元素的值替换要删除位置上的值--> [1,5,4,5,5] ---> 执行pop()，将最后的元素pop掉 --> [1,5,4,5]
    arrs[_index] = arrs[arrs.length -1];
    arrs.pop();
}
```

## Mapping Types
```solidity {.line-numbers}
mapping(address => uint) public balances;
//嵌套Mapping
mapping(address => mapping(address => bool)) public isFriend;

function examples() external {
    //向Mapping中添加Key-Value对
    balances[msg.sender] = 666;
    //获取值
    uint bal = balances[msg.sender];
    //当Key不存在Mapping中时，会返回Value对应的默认值
    uint bal2 = balances[address(1)]; // 0
    // delete 不会将Key-Value从Mapping中删除，只会将Value变为默认值
    delete balances[msg.sender];

    // 嵌套Mapping赋值
    isFriend[msg.sender][address(this)] = true;
}
```

### 迭代映射
```solidity {.line-numbers}
//使用循环遍历数组会消耗比较大的GAS费
mapping(address => uint) public balances;
mapping(address => bool) public inserted;
address[] public keys;

function set(address _key, uint _val) external {
    balances[_key] = _val;
    if(!inserted[_key]){
        inserted[_key] = true;
        keys.push(_key);
    }
}

function getSize() external view returns (uint) {
    return keys.length;
}

function first() external view returns (uint) {
    return balances[keys[0]];
}

function last() external view returns (uint) {
    return balances[keys[keys.length - 1]];
}

function get(uint _i) external view returns (uint) {
    return balances[keys[_i]];
}
```

# Function

Solidity 中有两个关键字， 标识函数的调用不用需要消耗gas: `view`和`pure`。  只有更改状态的时候才支付gas。

`view` and `pure` functions disallow modification of state.     
`pure` functions additionally disallow you to read from blockchain state.

If a gas calling function calls a `view` or `pure` function - only then will it cost gas. 如果一个要改变区块链状态的函数调用了`view`或者`pure`函数，才会消耗gas。

调用`view`函数是免费的，除非在消耗`gas`的函数中调用它。

如果一个函数是`view`函数，意味着我们只会读取这个合约的状态。`view函数`不允许修改任何状态。 `pure`函数还不允许读取区块链数据。

```solidity {.line-numbers}
uint256 public favoriteNumber;

function retrieve() public view returns(uint256){
    return favoriteNumber;
}

function add() public pure returns(uint256) {
    return (1+1);
}
```

## Function Visibility Specifiers
- `public`: 在外部和内部都可见(visible externally and internally)
- `private`: 表示只对合约内部可见(only visible in the current contract)
- `internal`: 表示只有这个合约或者继承它的合约可见(only visible internally)
- `external`: 表示只对合约外部可见(only for functions)，继承合约也看不到，如果在一个合约内部需要访问其external声明的函数，可以通过`this.`来进行访问, 但这种方式会浪费GAS费：
    ```solidity {.line-numbers}
    function externalFunc() external pure {
        // code...
    }
    function examples() external view{
        this.externalFunc();
    }
    ```


变量和函数如果没有指定可见度标识符，默认为`internal`。

## Function Modifier
函数修改器，可以用来将一些公共的函数功能提取到这里。

```solidity {.line-numbers}
contract FunctionModifier {
    bool public paused;
    uint public count;

    function setPaused(bool _paused) external {
        paused = _paused;
    }

    // 使用关键字modifier来定义一个函数修改器
    modifier whenNotPaused(){
        //这里表示，如果paused==false,则不再执行
        require(!paused, "paused");
        //必须有_;，它表示继续执行其函数体的代码
        _;
    }

    //添加 “whenNotPaused”，表示使用定义好的定义修改器 
    function inc() external whenNotPaused {
        count += 1;
    }

    function dec() external whenNotPaused {
        count -= 1;
    }

    //带参数的函数修改器
    modifier cap(uint _x){
        require(_x < 100, "x >= 100");
        _;
    }

    // 使用了2个函数修改器
    function incBy(uint _x) external whenNotPaused cap(_x) {
        count += _x;
    }
}
```

## Constructor 构造函数

`constructor`构造函数只在合约部署时会调用一次。
```solidity {.line-numbers}
contract ConstructorTest {
    // 表示部署者的地址
    address public owner;
    uint public x;

    constructor(uint _x) {
        owner = msg.sender;
        x = _x;
    }
}
```

## Fallback 回退函数
回退函数有两个功能：
- 当在合约中调动不存在的函数时，会调用**回退函数**
- 当向合约中发送主币时，会调用**回退函数**

回退函数有2种写法：

```solidity {.line-numbers}
contract Fallback {

    event Log(string func, address sender, uint value, bytes data);

    fallback() external payable {
        emit Log("fallback", msg.sender, msg.value, msg.data);
    }

    receive() external payable {
        emit Log("receive", msg.sender, msg.value, "");
    }
}
```
2种回退函数的调用关系：
![2种方法的调用关系](../images/fallback.png)


## 不可变变量 immutable
使用`immutable`声明的变量为不可变变量，不可变变量它能节约`GAS费`。它的赋值有2种方式：第一种：在声明时进行赋值，第二种：在构造函数中进行赋值。
```solidity {.line-numbers}
contract ImmutableExample {
    // 第一种：在声明时进行赋值
    address public immutable owner = msg.sender;

    address public immutable owner2;

    第二种：在构造函数中进行赋值
    constructor() {
        owner2 = msg.sender;
    }
}
```
## payable 关键字
一个函数如果标注了`payable`关键字，则此函数可以接受以太坊主币的传入。

一个`address`地址变量标注了`payable`关键字，则此地址变量可以发送主币了。

```solidity {.line-numbers}
contract PayableExample {
    address payable public owner;
    
    constructor() {
        // 由于msg.sender这个地址，是不具有发送主币的功能
        // 所以使用payable进行包装，让它具有发送主币的功能
        owner = payable(msg.sender);
    }

    // 向合约发送主币
    function deposit() external payable{}

    // 获取当前合约的余额
    function getBalance() external view returns (uint) {
        return address(this).balance;
    }
}
```

# Event 事件
`Event`事件是一种记录当前智能合约运行状态的方法，但它并不记录在状态变量中,而是会体现在区块链浏览器上或者是体现在交易记录中的logs里。

事件比使用状态变量来存储信息更节约GAS费。

```solidity {.line-numbers}
// 申明事件
event Log(string message, uint val);
// 使用 indexded 进行标识过的参数，在链外是可以进行搜索查询。
// 注意：在一个事件中，带索引indexed的参数最多为3个，超过3个就会报错。
event IndexedLog(address indexed sender, uint val); 

event Message(address indexed _from, address indexed _to, string message);

// 带有触发的方法，不能指定为view 或者 pure，因为事件也是需要在链上进行记录的
function examples() external {
    //使用 emit 来触发事件
    // 事件会被汇报到交易记录的logs里，同时也会体现在区块链浏览器上
    emit Log("foo", 123);

    emit IndexedLog(msg.sender, 1111);
}

function sendMessage(address _to, string calldata message) external {
    emit Message(msg.sender, _to, message); 
}
```

# Inherit 继承

- 单继承：

```solidity {.line-numbers}
contract A {
    // 添加 virtual 表示 子合约可以重写此函数 
    function foo() public pure virtual returns (string memory) {
        return "foo-A";
    }

    function bar() public pure virtual returns (string memory) {
        return "bar-A";
    }

    function baz() public pure returns (string memory) {
        return "baz-A";
    }
}

contract B is A {
    // 需要添加 override 表示重写父合约的函数，不加此项，会报错
    function foo() public pure override returns (string memory) {
        return "foo-B";
    }

    // 如果还需要让其他合约重写，就需要不回virtual，不管这个函数是不是重写自父合约
    function bar() public pure virtual override returns (string memory) {
        return "bar-B";
    }
}

contract C is B {
    function bar() public pure override returns (string memory) {
        return "bar-C";
    }
}
```

- 多继承：

要进行多继承时，一定要将最父级写在前面，然后再写次低级，依以类推下去。

```solidity {.line-numbers}
contract A {
    // 添加 virtual 表示 子合约可以重写此函数 
    function foo() public pure virtual returns (string memory) {
        return "foo-A";
    }

    function bar() public pure virtual returns (string memory) {
        return "bar-A";
    }

    function baz() public pure returns (string memory) {
        return "baz-A";
    }
}

contract B is A {
    // 需要添加 override 表示重写父合约的函数，不加此项，会报错
    function foo() public pure virtual override returns (string memory) {
        return "foo-B";
    }

    // 如果还需要让其他合约重写，就需要不回virtual，不管这个函数是不是重写自父合约
    function bar() public pure virtual override returns (string memory) {
        return "bar-B";
    }
}

contract D is A, B {
    // override(A,B)  表示要重写哪些父合约的相同函数， 
    // 如果所有父合约都有，并都写了virtual声明，则都需要加上 
    function foo() public pure override(A,B) returns (string memory) {
        return "foo-D";
    }
    function bar() public pure override(A,B) returns (string memory) {
        return "bar-D";
    }
}
```
- 继承构造函数带参数的父合约
```solidity {.line-numbers}
contract A {
    string public name;

    constructor(string memory _name) {
        name = _name;
    }
}

contract B {
    string public text;

    constructor(string memory _text) {
        text = _text;
    }
}

// 父级合约中的构造函数执行顺序，是按继承顺序来进行执行

// 第1种 给父级合约中带参数的构造函数传参
contract C is A("A"), B("B"){
    //code
}

// 第2种 给父级合约中带参数的构造函数传参
contract D is A, B {
    constructor(string memory _name, string memory _text) A(_name) B(_text) {
        // code
    }
}

// 第2种 给父级合约中带参数的构造函数传参
contract E is A("A"), B {
    constructor(string memory _text) B(_text) {
        //code
    }
}
```

如果要调用父合约中被重写的函数，可以通过**父合约的名称**或者`super`来调用。

# Errors & Warnings

`Warnings` won't stop your code from working but it's usually a good idea to check them out.

**3种报错**控制：`require`、`revert`、`assert`，这3种方式都会让`GAS费退回`和各种`状态回滚`。还有`自定义错误`，它可以节约GAS费。
```solidity {.line-numbers}
function testRequire(uint _i) public pure{
    // 表示当_i > 10 时，就报错，报错信息为："i > 10"
    require(_i <= 10, "i > 10");
}
```

`revert` 不能包含表达式。
```solidity {.line-numbers}
function testRevert(uint _i) public pure {
    if (_i > 10){
        revert("i > 10");
    }
}
```
`assert` 断言，不能提供报错信息
```solidity {.line-numbers}
function testAssert(uint _i) public pure {
    assert(_i <=10);
    //code
}
```


自定义报错：
```solidity {.line-numbers}
//使用关键字error进行自定义报错的定义
//使用自定义报错，可以节约GAS费
error MyError(address caller, uint i);
    
function testCustomErro(uint _i) public view {
    if (_i > 10){
        revert MyError(msg.sender, _i);
    }
}
```




# 数据的存储位置Data Locations
在智能合约中，数据可以存储在：`Memory`、`Storage`、`Calldata`中。

- 存储在`storage`中的是状态变量
- `memory`中的是局部变量，即在其函数或者其他的作用域内有效，而并不会被写入到链上，离开作用域即失效。
- `calldata`与`memory`类似，但它只能用在函数的输入参数中。在参数中使用`calldata`可以节约`GAS`费。

```solidity {.line-numbers}
struct MyStruct {
    uint foo;
    string text;
}

mapping(address => MyStruct) public myStructs;

// calldata 只能用在输入参数中，并且使用calldata可以节约GAS费
// 在参数中有数组、字符串、结构体时，必须给参数加上calldata或者memory
function examples(uint[] calldata y, string calldata s, MyStruct calldata _mystruct) external returns (uint[] memory) {
    myStructs[msg.sender] = MyStruct({foo: 123, text: "bar"});
    MyStruct storage myStruct = myStructs[msg.sender];
    // 会修改链上的数据状态
    myStruct.text = "foo";

    MyStruct memory readOnlyStruct = myStructs[msg.sender];
    // 并不会修改链上的状态
    readOnlyStruct.foo = 353;

    uint[] memory memArr = new uint[](3);
    memArr[0] = 332;

    return memArr;
}
```
```solidity {.line-numbers}
struct Todo{
    string text;
    bool completed;
}

Todo[] public todos;

function create(string calldata _text) external {
    todos.push(Todo({
        text: _text,
        completed: false
    })); 
}

function updateText(uint _index, string calldata _text) external {
    // 当只有一个数据需要进行更新时，使用这种方法会比较节约GAS费
    todos[_index].text = _text;

    // // 如果有多个数据需要进行更新，则使用这种方法比较节约GAS费
    // // 首先将需要更新的对象读取到storage 对象中，再进行更新操作
    // Todo storage todo = todos[_index];
    // todo.text = _text; 
    // todo.text = _text; 
    // todo.text = _text; 
}

function get(uint _index) external view returns (string memory, bool){
    // 这里使用storage比memory更节约GAS费，因为storage时是直接从状态变量中读取出来的，通过一次拷贝即可返回
    // 使用memory时，则会进行两次拷贝，所以更耗GAS费
    // Todo memory todo = todos[_index];
    Todo storage todo = todos[_index];
    return (todo.text, todo.completed); 

    //比上面的方式进行返回，这种会消耗更多的GAS
    // return (todos[_index].text, todos[_index].completed);
}

function toggleCompleted(uint _index) external {
    todos[_index].completed = !todos[_index].completed;
}
```

# 合约操作

## 1、合约中发送主币的方法
- `transfer`: 只会带有2300个GAS，如果失败就会revert
- `send`: 只会带有2300个GAS，会返回一个bool来标识是否成功
- `call`: 会发送所有剩余的GAS，会返回一个boolgo标识是否成功，还有一个data。

```solidity {.line-numbers}
// 用于发送主币的合约
contract SendEther {
    //通过构造函数，让在部署合约时，使合约中有一定的主币数量
    constructor() payable {}

    receive() external payable{}

    // 通过 transfer()函数发送主币
    function sendViaTransfer(address payable _to) external payable {
        // 123 表示 123Wei
        _to.transfer(123);
    }

    // 通过 send()函数发送主币
    function sendViaSend(address payable _to) external payable {
        bool sent =  _to.send(123);
        require(sent, "send failed");
    }

    // 通过 call()函数发送主币
    function sendViaCall(address payable _to) external payable {
        (bool success,) = _to.call{value: 123}("");
        require(success, "fall failed");
    }

    // 返回合约剩余的主币数额， 单位为Wei
    function getBalance() external view returns (uint) {
        return address(this).balance;
    }
}

// 用于接收主币的合约
contract EthReceiver {
    // 通过事件记录，接收到的主币信息
    /**
    * amount: 接收到的主币数量(单位为Wei)
    * gas: 剩余的 gas 
    */
    event Log(uint amount, uint gas);

    // 当接收到主币时，会调用receive()
    receive() external payable {
        emit Log(msg.value, gasleft());
    }

    // 返回合约剩余的主币数额， 单位为Wei
    function getBalance() external view returns (uint) {
        return address(this).balance;
    }
}
```
## 2、从合约中提款
```solidity {.line-numbers}

contract EtherWallet {
    // 合约拥有者
    address payable public immutable owner;

    // 通过事件记录，接收到的主币信息
    /**
    * amount: 接收到的主币数量(单位为Wei)
    * gas: 剩余的 gas 
    */
    event Log(uint amount, uint gas);

    constructor() payable {
        // 通过构造函数来设置合约的拥有者
        owner = payable(msg.sender);
    }

    // 当合约接收到主币时，会调用
    receive() external payable {
        emit Log(msg.value, gasleft());
    }

    // 从合约中提款
    function withdraw(uint _amount) external {
        // 只有合约的拥有者才能进行提款
        require(msg.sender == owner, "caller is not owner");

        payable(msg.sender).transfer(_amount);

        // // call()函数不需要发送者具有payable属性也可以进行发送主币
        // (bool success, ) = msg.sender.call{value: _amount}("");
        // require(success, "Failed to send Ether");
    }

    // 获取合约中的主币余额,单位为Wei
    function getBalance() public view returns (uint) {
        return address(this).balance;
    }
}
```
## 调用其他合约
```solidity {.line-numbers}
contract CallTestContract {

    // 通过合约的地址来，实例化目标合约对象
    function setX(address  _test, uint _x) external {
        TestContract(_test).setX(_x);
    }

    // 直接将目标合约对象以参数形式进行传递
    function setX2(TestContract _test, uint _x) external {
        _test.setX(_x);
    }

    function getX(address  _test) external view returns (uint) {
        return TestContract(_test).getX();
    }

    function getXandValue(address  _test) external view returns (uint, uint) {
        return TestContract(_test).getXandValue();
    }

    // 向目标合约操作带发送主币功能
    function setXandSendEther(address  _test, uint _x) external payable  {
        TestContract(_test).setXandReceiveEther{value: msg.value}(_x);
    }
}

contract TestContract {
    uint public x;
    uint public value = 123; 

    function setX(uint _x) external {
        x = _x;
    }

    function getX() external view returns (uint) {
        return x;
    }

    function setXandReceiveEther(uint _x) external payable {
        x = _x;

        value = msg.value;
    }

    function getXandValue() external view returns (uint, uint) {
        return (x, value);
    }
}
```

## 通过 Interface 接口调用其他合约

有时，我们并不知道一个合约的原代码，或者它的代码非常大，此时，我们可以通过`Interface`来调用。

```solidity {.line-numbers}
// 目标调用合约
contract Counter {
    uint public count;

    function inc() external {
        count += 1;
    }

    function dec() external {
        count -= 1;
    }
} 

// 接口
interface ICounter {
    function count() external view returns (uint);
    function inc() external;
}

contract CallInterface {
    uint public count;

    // 参数为被调用的合约的地址
    function examples(address _counter) external {
        ICounter(_counter).inc();
        count = ICounter(_counter).count();
    }
}
```

## 通过 call() 调用其他合约

```solidity {.line-numbers}
contract TestCall {
    string public message;
    uint public x;

    event Log(string message);

    // 如果调用了这个合约中不存在的函数，就会触发fallback()回退函数
    // 如果调用这个合约中的函数时，存在发送主币，此时也会调用fallback()函数
    fallback() external payable {
        emit Log("fallback was called");
    }

    function foo(string memory _message, uint _x) external payable returns (bool, uint) {
        message = _message;
        x = _x;
        return (true, 999);
    }
}

contract Call {

    bytes public data;

    /*
     * 调用一个地址的call()时，通过abi.encodeWithSignature来调用该合约中的函数
    */
    function callFoo(address _test) external payable {
        (bool success, bytes memory _data) = _test.call{value: 111}(abi.encodeWithSignature("foo(string, uint256)", "call foo", 123));
        require(success, "call failed");

        data = _data;
    }

    //调用合约中不存在的函数
    function callDoseNotExitFuc(address _test) external payable {
        (bool success,) = _test.call(abi.encodeWithSignature("doesNotExitFuc()"));
        require(success, "call failed");
    }
}
```


---

`EVM` -- `Ethereum Virtual Machine`

部署到`EVM`上的`solidity`程序，可以部署到`Avalanche`、`Fantom`、`Polygon`区块链上。

`EVM` can access and store information in six places:
- Stack
- Memory
- Storage
- Calldata
- Code
- Logs


`ABI` -- Application Binary Interface