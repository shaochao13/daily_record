
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

### Array

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
- `external`: 表示只对合约外部可见(only for functions)
- `internal`: 表示只有这个合约或者继承它的合约可见(only visible internally)

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


# Memory, Storage & Calldata

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