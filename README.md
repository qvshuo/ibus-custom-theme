# ibus-custom-theme
非Gnome桌面环境，自定义ibus输入法的字体、字号和配色。

---

Archlinux Wiki中只给出了Gnome桌面环境通过修改gnome-shell主题实现上述功能的描述，而该方法并不适用于其他情形。

在非Gnome桌面环境下，ibus的显示效果是由当前Gtk主题确定的。而`$HOME/.config/gtk-3.0/settings.ini`文件定义了当前的Gtk3主题及字体字号。该文件的部分内容示例如下：

```
[Settings]
gtk-theme-name=Materia-light
gtk-font-name=更纱黑体 SC 12
```

上述表述中，`gtk-theme-name`指定了当前Gtk主题为`Materia-light`，`gtk-font-name`指定了当前的字体为`更纱黑体 SC`，字号为`12`。

可通过修改上述文件实现改变ibus字体和字号的目的。

至于ibus的配色方案，可以在ibus启动的时候指定其使用特定Gtk3主题，即可实现对ibus配色的自定义。

于是创建一个名为`ibus-custom-theme`的Gtk3主题：

`mkdir -p $HOME/.theme/ibus-custom-theme/gtk-3.0`

`$EDITOR $HOME/.theme/ibus-custom-theme/gtk-3.0/gtk.css`

文件内容示例：

```
* {
  color: #0b141a; /* 字体颜色 */
  background-color: #ffffff; /* 背景颜色 */
  -gtk-secondary-caret-color: #d4d4d4; /* 高亮背景颜色 */
}
```


之后，修改ibus输入法的自启命令，比如写在`$/HOME/.xinitrc`中：

`$EDITOR $HOME/.xinitrc`

键入：

```
GTK_THEME=ibus-custom-theme ibus-daemon -dx &
```

最后执行下方命令即可立刻生效：

`kill ibus-daemon && GTK_THEME=ibus-custom-theme ibus-daemon -dx &`
