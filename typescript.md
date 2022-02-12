
## `tsconfig.json` 配置

```json
{
  "compilerOptions": {
    "noEmitOnError": true, // 源文件代码出错，则不生成文件
    "declaration": true, // 自动生成对应的 *.d.ts 文件
  }
}
```

## 工具泛型

以下所有例子以这个源为例

```typescript
interface UserProps {
  name: string
  nickname: string
  age: number
}
```

1. Pick

    > Pick<Type, Keys>  
    > 取 keys 值

    ```typescript
    type NewUserProps = Pick<UserProps, 'name'> 
    // 等同于 
    { 
      name: string
    }
    ```
1. Omit 

    > Omit<Type, Keys>  
    > 排除 keys 以外的值

    ```typescript
    type NewUserProps = Omit<UserProps, 'name'> 
    // 等同于 
    { 
      nickname: string
      age: number 
    }
    ```
1. Readonly

    > Readonly<Type>
    > 只读

    ```typescript
    const user: Readonly<UserProps> = {
      name: 'name',
      nickname: 'nickname',
      age: 10,
    }
    // 无法分配到 "name" ，因为它是只读属性。
    user.name = 'name2'
    ```
1. ReadonlyArray

    > ReadonlyArray<Type>
    > 只读

    ```typescript
    const foo: number[] = [1, 2, 3, 4]
    const bar = ReadonlyArray<number> = foo

    bar[0] = 10 // error!
    bar.push(10) // error!
    bar.length = 3 // error!
    ```

1. Required

    > 将可选变成必选  
    ```typescript
    interface UserProps {
      name: string
      age?: number
    }
    const user: Required<UserProps> = {
      name: 'haha',
      age: 100
    }
    ```

1. Record

    > Record<Keys, Type>  
    > 将一个类型属性映射到另一个类型时

    ```typescript
    interface User { name: string }
    const users: Record<string, User> = {
      info: {
        name: 'haha'
      },
      info2: {
        name: 'haha2'
      }
    }
    ```

1. Partial

    > 变成可选

    ```typescript
  const user: Partial<UserProps> = {
    name: 'haha'
  }
    ```


## 条件类型

1. ReturnType

1. Extract

1. Exclude

1. as const

  > 不可修改  
  ```typescript
  const foo = { bar: 'baz' } as const
  foo.bar = 123 // Error!
  ```

