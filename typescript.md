
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

    > Pick<type, keys>  
    > 取 keys 值

    ```typescript
    type NewUserProps = Pick<UserProps, 'name'> 
    // 等同于 
    { 
      name: string
    }
    ```
1. Omit 

    > Omit<type, keys>  
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

    > Readonly<type>
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

    > ReadonlyArray<type>
    > 只读

    ```typescript
    const foo: number[] = [1, 2, 3, 4]
    const bar = ReadonlyArray<number> = foo

    bar[0] = 10 // error!
    bar.push(10) // error!
    bar.length = 3 // error!
    ```

1. Required
1. Record
1. Partial

## 条件类型

1. ReturnType



1. Extract

1. Exclude

