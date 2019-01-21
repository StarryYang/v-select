# v-select

> it is to keep the same displaying on the ios and android

## Build Setup

```bash
# install dependencies
npm install --save yh-select

# Template
<v-select name="school" v-model="school" :sel="school" :options="list" :val="val" :names="name"></v-select>

v-model 值须与 sel一致
options 循环的option 数组
val 指定option的value值
names 指定option的显示文字
```
