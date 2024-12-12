
有同事反映，在Pro中新建要素类时，没办法设定名称为“新建”，会自己变成不完整的拼音。
查看了一下，确有此事。
在相同的界面里还有其他输入框，却没有这种情况。
研究了一下，发现是输入法引发的连锁问题。
有问题的输入框，是加了数据验证的。因为pro中创建要素类时，不允许名称中带特殊字符，防止引发系统路径异常。
而微软中文输入法，恰恰踩了这个雷。
写一段测试代码，创建一个wpf程序，监控textbox的TextChanged事件。



```
private void TextBox_TextChanged(object sender, TextChangedEventArgs e)
{
    Debug.WriteLine((sender as TextBox)?.Text);
}

```

当使用微软中文输入法，输入xinjian\+空格的时候，输入如下



```
x
xi
xin
xin'j
xin'ji
xin'jia
xin'jian
新建
新建

```

而使用搜狗输入法的时候，输入如下



```
新建
新建

```

所以，微软输入法在键盘键入过程中，也触发了TextChanged事件，导致了单引号的引入，触发了数据验证的过程，所以出现了这个问题。
最好的办法，还是换输入法吧。(\#.\#)


 本博客参考[wgetcloud加速器官网下载](https://longdu.org)。转载请注明出处！
