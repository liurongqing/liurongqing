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

1. [Pick](#Pick)
1. [Omit](#Omit)
1. [Readonly](#Readonly)
1. [ReadonlyArray](#ReadonlyArray)
1. [Required](#Required)
1. [Record](#Record)
1. [Partial](#Partial)
1. [ReturnType](#ReturnType)
1. [Parameters](#Parameters)
1. [Extract](#Extract)
1. [Exclude](#Exclude)
1. [as const](#as const)
1. [keyof](#keyof)
1. [extends](#extends)
1. [ReadonlyArray](#ReadonlyArray)
1. [in](#in)

以下所有例子以这个源为例

```typescript
interface UserProps {
  name: string
  nickname: string
  age: number
}
```

## Pick

> Pick<Type, Keys>  
> 取 keys 值

```typescript
type NewUserProps = Pick<UserProps, 'name'>
// 等同于
{
  name: string
}
```

## Omit

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

## Readonly

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

## ReadonlyArray

> ReadonlyArray<Type>
> 只读

```typescript
const foo: number[] = [1, 2, 3, 4]
const bar = ReadonlyArray<number> = foo

bar[0] = 10 // error!
bar.push(10) // error!
bar.length = 3 // error!
```

## Required

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

## Record

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

## Partial

> Partial<Type>
> 变成可选

```typescript
const user: Partial<UserProps> = {
  name: 'haha',
}
```

## ReturnType

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

## Parameters

> Parameters<Type>  
> 取函数的参数类型

```typescript
type TypeA = Parameters<(options: { a: string }) => any>
// [options: { a: string }]
```

## Extract

> Extract<Type, Union>  
> 取交集

```typescript
type Width = string | number
type WidthType = Extract<Width, string>
// string
```

## Exclude

> Exclude<Type, ExcludeUnion>
> 取差集

```typescript
type Width = string | number
type WidthType = Exclude<Width, string>
// number
```

## as const

> 不可修改

```typescript
const foo = { bar: 'baz' } as const
foo.bar = 123 // Error!
```

## keyof

> 获取接口的 key 的联合类型

```typescript
type keys = keyof UserProps
// 'name' | 'nickname' | 'age'
```

## extends

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

## 条件类型

> U ? X : Y

```typescript
type Extract<T, U> = T extends U ? T : never
```

## in

> 类型映射

```typescript
type Readonly<T> = {
  readonly [P in keyof T]: T[p]
}
```
