# Symbol
1. 表示独一无二的值。
2. 通过Symbol函数产生。原来对象的属性名只能是字符串，现在增加了Symbol类型。
3. 可以用typeof检测，会打印出是Symbol类型。
4. Symbol函数前不能用new运算符，Symbol是原始类型，不是对象
5. 可以接受字符算做参数，这样是为了打印的时候比较好区分。
> 果Symbol参数是一个对象，就会调用该对象的toString方法，将其转为字符串，然后才生成一个Symbol值。
> const obj={
>   toString(){
>    return 'abc';
>   }
> }
> const sym  = Symbol(obj);
> sym //Symbol(abc)

6. Symbol作为属性名，不能用.运算符，在对象内部，Symbol值必须放在方括号之中。
7.【增强对象写法】
8. 性名的遍历。不会出现在for...in,for...of循环中，不会被Obejct.keys(),Obejct.getOwnPropertyNames(),Json.stringfy()返回。
他可以用Object。getOwnPropertySymbols方法，获取【指定对象】的所有Symbol属性名
9. API，返回所有键名。Reflect.ownKeys可以返回所有类型的键名。
