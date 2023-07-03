项目中相关的Qt知识

QVariant

```c++
 QVariant v;

 MyCustomStruct c;
 if (v.canConvert<MyCustomStruct>())
     c = v.value<MyCustomStruct>();

 v = 7;
 int i = v.value<int>();                        // same as v.toInt()
 QString s = v.value<QString>();                // same as v.toString(), s is now "7"
 MyCustomStruct c2 = v.value<MyCustomStruct>(); // conversion failed, c2 is empty

```

 QVariant.value<QString>：将QVariant类型转换成QString类型



QVariant::fromValue(s)，将某类型的值包装成QVariant类型，

```
 MyCustomStruct s;
 return QVariant::fromValue(s);

```

