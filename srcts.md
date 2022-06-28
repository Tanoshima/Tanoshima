## yup add custom method

```/yup/custom-validation.ts
// /yup/custom-validation.ts
import * as Yup from 'yup'
import './locale'

Yup.addMethod<Yup.StringSchema>(Yup.string, 'hiragana', function () {
  return this.test(
    'hiragana',
    'ひらがなで入力して下さい',
    function (value: any) {
      if (value == null || value === '') return true
      return value.match(/^[ぁ-んー]+$/)
    }
  )
})
```
```yupを使うファイル.tsx
// yupを使うファイル.tsx

// この記述がないと型エラーになる
declare module 'yup' {
  interface StringSchema {
    hiragana(this: StringSchema): StringSchema
  }
}

const schema = yup.object({
  hiragana: yup.string().hiragana(),
})
```
