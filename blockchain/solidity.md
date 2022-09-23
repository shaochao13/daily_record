# `Types`

Solidity is a statically language.

## `Value Types`

### `Booleans`

### `Integers`

uint/int

### `Address`

## `Reference Types`

### `Struct`

### `Array`

# `Function`

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


# `Errors & Warnings`

`Warnings` won't stop your code from working but it's usually a good idea to check them out.