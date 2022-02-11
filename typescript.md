
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

```js
interface UserProps {
  name: string
  nickname: string
  age: number
}
```

Partial

Required

Readonly

1. Pick

    > Pick<type, keys>   
    > 取 keys 值

    ```js
    type NewUserProps = Pick<UserProps, 'name'> 
    // 等同于 
    { 
      name: string
    }
    ```
1. Omit 

    > Omit<type, keys>
    > 排除 keys 以外的值

    ```js
    type NewUserProps = Omit<UserProps, 'name'> 
    // 等同于 
    { 
      nickname: string
      age: number 
    }
    ```

Record

## 条件类型

1. ReturnType



1. Extract

1. Exclude

