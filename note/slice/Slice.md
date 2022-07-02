# Slice

- 与数组不同，slice 的类型仅由它所包含的元素的类型决定（与元素个数无关）。(数组与元素个数相关)

  ```go
  // 如何声明
  s := make([]string, 3)
  t := []string{"g", "h", "i"}
  
  // 二维slice
  twoD := make([][]int, 3)
  for i := 0; i < 3; i++ {
  	innerLen := i + 1
  	twoD[i] = make([]int, innerLen)
  	for j := 0; j < innerLen; j++ {
  		twoD[i][j] = i + j
  	}
  }
  ```

- Slice 可以组成多维数据结构。**内部的 slice 长度可以不一致**，这一点和多维数组不同。

- 比如 slice 支持内建函数 `append`， 该函数会返回一个包含了一个或者多个新值的 slice。 注意由于 `append` 可能返回一个新的 slice，我们需要**接收其返回值**。（突破cap，新建slice）

- slice 还可以 `copy`。（底层不共享）

- slice 支持通过 `slice[low:high]` 语法进行“切片”操作。 （底层地址共享）

- 注意，slice 和数组是不同的类型，但它们通过 `fmt.Println` 打印的输出结果是类似的。

- [go 官方博客-slice实现细节](https://go.dev/blog/slices-intro)

  - slice 内存泄漏 官方提出解决方法之一是`copy()`

    ```go
    b = make([]int, 100)
    
    // copy
    a = b[:2] // a 可能通过函数返回一个来自b的byte[]切片
    c = make([]int, len(a)）
    copy(c, a)
    // 之后a,b不再使用，gc回收
    ```

    

  - 另外也提了一句使用`append()`解决：可以看看煎鱼的文章

    ```go
    b = make([]int, 100)
    
    a = []int
    a = append(a, b[:2]...)
    // b = nil
    // 或者b不再使用被gc回收
    ```

- nil slice vs empty slice

  - ```go
    a = make([]int, 100)
    a = nil
    
    b = make([]int, 100)
    b = b[:0]
    ```

  - nil slice 的长度len和容量cap都是0

  - empty slice的长度是0, 容量是由指向底层数组决定

  - empty slice != nil

  - nil slice的pointer 是nil, empty slice的pointer是底层数组的地址(empty slice可能内存泄漏)