# 页面传值

## List
- 前台传数组，后台接收数组
```text
// 前台
var ids[]=[1,2,3,4,5,6]
data:{ids:ids},
// 后台
@ResponseBody
public String xxx(@RequestParam(value = "ids[]") Integer[] ids){}
// 后台接收类型Integer[]也可以是String[]或者是List<Integer>和List<String>
```
- 数组转换成JSON字符串，后台接收字符串，然后再对字符串进行处理。
- 传多个参数+值，后台直接接收LIst。

## 参考
- [ajax传参数组,spring boot 接收](https://www.jianshu.com/p/85251b746058)