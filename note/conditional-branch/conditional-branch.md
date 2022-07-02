# conditional-branch

### if-else

- 在条件语句之前可以有一个声明语句；在这里声明的变量可以在这个语句所有的条件分支中使用。
- Go 没有**三目运算符**， 即使是基本的条件判断，依然需要使用完整的 `if` 语句。

### switch

- 在同一个 `case` 语句中，你可以使用逗号来分隔多个表达式。

- 不带表达式的 `switch` 是实现 if/else 逻辑的另一种方式。

-  `case` 表达式也可以不使用常量。

- 类型开关 (`type switch`) 比较类型而非值。可以用来发现一个接口值的类型。

  ```go
  whatAmI := func(i interface{}) {
  	switch t := i.(type) {
  	case bool:
  		fmt.Println("I'm a bool")
  	case int:
  		fmt.Println("I'm an int")
  	default:
  		fmt.Printf("Don't know type %T\n", t)
  	}
  }
  ```

  