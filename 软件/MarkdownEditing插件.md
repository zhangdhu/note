MarkdownEditing的功能

下面将列出MarkdownEditing提供的功能。

语法增强类

星号*、下划线_和反引号`自动配对
如输入的自动配对符号中间内容为空时，删除第一个符号时将直接删除整对符号
如输入自动配对符号后直接输入空格，则自动删除后面自动配对的符号
波浪线 ~ 包围的内容将转换为HTML中的 <del></del> 标签
当创建了列表后，回车将自动添加一个列表项。如列表项为空，再次回车将删除该列表项
快捷键类（根据自行修改的Default (Windows).sublime-keymap列出）

MarkdownEditing在Windows下面的快捷键需要自行根据Default (OSX).sublime-keymap中的内容进行修改，添加到Default (Windows).sublime-keymap中。

Ctrl+Win+V 选中的内容将自动转换为行内式超链接，链接到剪贴板中的内容
Ctrl+Win+R 选中的内容将自动转换为参考式超链接，链接到剪贴板中的内容
Ctrl+Alt+R 弹出提示框插入一个参考式超链接，在提示框中输入链接内容和定义参考ID[^3]
Ctrl+Win+K 插入一个标准的行内式超链接
Win+Shift+K 插入一个标准的行内式图片（此快捷键可能与输入法有冲突）
Ctrl+1 至 Ctrl+6 插入一级至六级标题
Win+Alt+i 选中的内容转换为斜体
Win+Alt+b 选中的内容转换为粗体[^1]
Ctrl+Shift+6 自动插入一个脚注，并跳转到该脚注的定义中。
Alt+Shift+F 查找没有定义的脚注并自动添加其定义链接
Alt+Shift+G 查找没有定义的参考式超链接并自动添加其定义链接
Ctrl+Alt+S 脚注排序
Ctrl+Shift+. 缩进当前内容
Ctrl+Shift+, 提前当前内容