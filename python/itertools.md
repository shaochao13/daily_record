- `itertools.compress(it, selector_it)`

    并行处理两个可迭代的对象：如果 `selector_it` 中的元素是真值，产出 `it`中对应的元素
    ```python
    def vowel(c):
        return c.lower() in 'aeiou'

    s = 'Aardvark'

    list(itertools.compress(s, (1,0,1,1,0,1)))
    #out: ['A', 'r', 'd', 'a']
    ```

- `itertools.accumulate(it, [func])`

    产出累积的总和：如果提供了`func`，那么把前两个元素传给它，然后把计算结果和下一个元素会给它，以此类推，最后产出结果。

    ```python
    import itertools

    sample = [5, 4, 2, 8, 7, 6, 3, 0, 9, 1]
    list(itertools.accumulate(sample))
    #out:[5, 9, 11, 19, 26, 32, 35, 35, 44, 45]

    list(itertools.accumulate(sample, min))
    #out:[5, 4, 2, 2, 2, 2, 2, 0, 0, 0]

    list(itertools.accumulate(sample, max))
    #out:[5, 5, 5, 8, 8, 8, 8, 8, 9, 9]

    import operator
    list(itertools.accumulate(sample, operator.mul))
    #out: [5, 20, 40, 320, 2240, 13440, 40320, 0, 0, 0]
    ```

- `itertools.starmap(func, it)`

    ```python
    list(itertools.starmap(operator.mul, enumerate('albatroz', 1)))
    #out:['a', 'll', 'bbb', 'aaaa', 'ttttt', 'rrrrrr', 'ooooooo', 'zzzzzzzz']

    sample = [5,4,2,8,7,6,3,0,9,1]
    list(itertools.starmap(lambda a, b: b/a, enumerate(itertools.accumulate(sample), 1)))
    #out:[5.0,4.5,3.6666666666666665, 4.75, 5.2,5.333333333333333,5.0,4.375,4.888888888888889,4.5]
    ```

- `itertoos.product(it1, ..., itN, repeat=1)` 计算笛卡儿积
    ```python
    list(itertools.product('ABC', range(2)))
    #out:[('A', 0), ('A', 1), ('B', 0), ('B', 1), ('C', 0), ('C', 1)]

    suits = 'spades hearts diamonds clubs'.split()
    list(itertools.product('AK', suits))
    #out:[(' A', 'spades'), (' A', 'hearts'), (' A', 'diamonds'), (' A', 'clubs'), (' K', 'spades'), (' K', 'hearts'), (' K', 'diamonds'), (' K', 'clubs')]

    list(itertools.product("ABC", repeat=2))
    #out:[(' A', 'A'), (' A', 'B'), (' A', 'C'), (' B', 'A'), (' B', 'B'), (' B', 'C'), (' C', 'A'), (' C', 'B'), (' C', 'C')]

    list(itertools.product('AB', range(2), repeat=2))
    #out:(' A', 0, 'A', 0) (' A', 0, 'A', 1) (' A', 0, 'B', 0) (' A', 0, 'B', 1) (' A', 1, 'A', 0) (' A', 1, 'A', 1) (' A', 1, 'B', 0) (' A', 1, 'B', 1) (' B', 0, 'A', 0) (' B', 0, 'A', 1) (' B', 0, 'B', 0) (' B', 0, 'B', 1) (' B', 1, 'A', 0) (' B', 1, 'A', 1) (' B', 1, 'B', 0) (' B', 1, 'B', 1)

    ```

- `itertools.groupby(it, key=None)`

    产出由两个元素组成的元素， 形式为(key, group) ,key是分组标准;group是生成器,用于产出分组里的元素。

    ```python
    for char, group in itertools.groupby("LLLLLAAACCCCCGGGG"):
        print(char, '->', list(group))
    #out:
    '''
    L -> ['L', 'L', 'L', 'L', 'L']
    A -> ['A', 'A', 'A']
    C -> ['C', 'C', 'C', 'C', 'C']
    G -> ['G', 'G', 'G', 'G']
    '''


    animals = ['duck', 'eagle', 'rat', 'giraffe', 'bear', 'bat', 'dolphin', 'shark', 'lion']
    for length, group in itertools.groupby(animals, len):
        print(length, '->', list(group))
    #out:
    '''
    4 -> ['duck']
    5 -> ['eagle']
    3 -> ['rat']
    7 -> ['giraffe']
    4 -> ['bear']
    3 -> ['bat']
    7 -> ['dolphin']
    5 -> ['shark']
    4 -> ['lion']
    '''
    ```

- `itertools.tee(it, n=2)`

    产出一个由n个生成器组成的元组，每个生成器用于单独产出输入的可迭代对象中的元素

    ```python
    g1, g2 = itertools.tee("ABC")
    g1, g2
    #out:(['A', 'B', 'C'], ['A', 'B', 'C'])
    ```
- `itertools.reduce(func, it, [initial])`

    把前两个元素传给func, 然后把计算结果和第三个元素传给func, 以此类推，返回最后的结果；如果提供了initial、把它当作第一个元素传入。
