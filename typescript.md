## `tsconfig.json` 配置

```json
{
  "compilerOptions": {
    "noEmitOnError": true, // 源文件代码出错，则不生成文件
    "declaration": true // 自动生成对应的 *.d.ts 文件
  }
}
```

## 高级类型

[Pick](#Pick)

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

   > Required<Type>
   > 将可选变成必选

   ```typescript
   interface UserProps {
     name: string
     age?: number
   }
   const user: Required<UserProps> = {
     name: 'haha',
     age: 100,
   }
   ```

1. Record

   > Record<Keys, Type>  
   > 将一个类型属性映射到另一个类型时

   ```typescript
   interface User {
     name: string
   }
   const users: Record<string, User> = {
     info: {
       name: 'haha',
     },
     info2: {
       name: 'haha2',
     },
   }
   ```

1. Partial

   > Partial<Type>
   > 变成可选

   ```typescript
   const user: Partial<UserProps> = {
     name: 'haha',
   }
   ```

1. ReturnType

   > ReturnType<Type>
   > 取函数返回值类型

   ```typescript
   function func() {
     return {
       a: 1,
       b: 'haha',
     }
   }
   type typeA = ReturnType<() => number> // number
   type typeB = ReturnType<typeof func>
   /* {
     a: number
     b: string
   }*/
   ```

1. Parameters

   > Parameters<Type>  
   > 取函数的参数类型

   ```typescript
   type TypeA = Parameters<(options: { a: string }) => any>
   // [options: { a: string }]
   ```

1. Extract

   > Extract<Type, Union>  
   > 取交集

   ```typescript
   type Width = string | number
   type WidthType = Extract<Width, string>
   // string
   ```

1. Exclude

   > Exclude<Type, ExcludeUnion>
   > 取差集

   ```typescript
   type Width = string | number
   type WidthType = Exclude<Width, string>
   // number
   ```

1. as const

   > 不可修改

   ```typescript
   const foo = { bar: 'baz' } as const
   foo.bar = 123 // Error!
   ```

1. keyof

   > 获取接口的 key 的联合类型

   ```typescript
   type keys = keyof UserProps
   // 'name' | 'nickname' | 'age'
   ```

1. extends

   > 类型约束

   ```typescript
   interface length {
     length: number
   }
   function identity<T extends length>(arg: T): T {
     console.log(arg.length)
     return arg
   }
   ```

1. U ? X : Y

   > 条件类型

   ```typescript
   type Extract<T, U> = T extends U ? T : never
   ```

1. in

   > 类型映射

   ```typescript
   type Readonly<T> = {
     readonly [P in keyof T]: T[p]
   }
   ```
