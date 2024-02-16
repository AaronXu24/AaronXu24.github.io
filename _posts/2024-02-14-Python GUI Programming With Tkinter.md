---
layout: post
title: Python GUI Programming With Tkinter
subtitle: 根据原网站内容做了一些增补
excerpt_image: 
categories: Python
tags: [Tkinter]
top: 
---

**REF**: [Real python](https://realpython.com/python-gui-tkinter/)
- Several strengths:
	- **cross-platform**: so the same code works on Windows, macOS, and Linux.
	- Applications built with Tkinter look like they belong on the platform where they’re run: Visual elements are rendered using native operating system elements

# Building Your First Python GUI Application With Tkinter

- **Windows**:
	- The foundational element of a Tkinter GUI
	- The containers in which all other GUI elements live. 
		- **widgets**: These other GUI elements: such as text boxes, labels, and buttons

- **导入模块**：`import tkinter as tk`
- **添加一个窗口**：A **window** is an instance of Tkinter’s `Tk` class. Go ahead and create a new window and assign it to the [variable](https://realpython.com/python-variables/) `window`: `window = tk.Tk()`
- **添加一个小部件（widget）**：用tk.Label添加一些文字。`greeting = tk.Label(text="Hello, Tkinter")`。
	- 这样并不会在窗口上添加文字，因为你仅仅创建了一个Label对象，它和window并没有实际的交集。
	- 我们必须将Label添加到window上，我们有多种方法，以下为其中的一种：`greeting.pack()`。
	- 当您将小部件打包到窗口中时，Tkinter 将窗口调整得尽可能小，同时仍然完全包围小部件。
	- 添加以下命令：`window.mainloop()`。
		- `window.mainloop()` 告诉 Python 运行 Tkinter event loop（事件循环）。此方法侦听事件，例如按钮单击或按键，并阻止其后的任何代码运行，直到您关闭调用该方法的窗口为止。

参考代码：
```Python
import tkinter as tk

window = tk.Tk()
label = tk.Label(text="Python rocks!")
label.pack()

window.mainloop()
```

# 用小部件进行设计 Working With Widgets
- 小部件（widgets）是Python GUI框架的基石。每一种小部件都是由类定义的。以下是可供使用的一些小部件：

| Widget Class | Description |
| :--: | ---- |
| `Label` | A widget used to display text on the screen |
| `Button` | A button that can contain text and can perform an action when clicked |
| `Entry` | A text entry widget that allows only a single line of text |
| `Text` | A text entry widget that allows multiline text entry |
| `Frame` | A rectangular region used to group related widgets or provide padding between widgets |

# Label部件：

- 用来显示**文字**或者**图片**
- 用户（user）无法编辑该部件的文字，该部件仅做显示使用
- 如果不指定，Label会以默认的颜色和背景进行显示。
```python
	label = tk.Label(
    text="Hello, Tkinter",
    foreground="white",  # Set the text color to white
    background="black"  # Set the background color to black
)
```
- 可以通过设置进行调整，以下有多种颜色可以供选择：
	-  `"red"`
	- `"orange"`
	- `"yellow"`
	- `"green"`
	- `"blue"`
	- `"purple"`
	- 【Note】：
		- 大部分的[HTML颜色名字](https://htmlcolorcodes.com/color-names/)，对Tkinker都是起作用的。
		- [colors manual page](https://www.tcl.tk/man/tcl/TkCmd/colors.html)也可以供查阅
		- 十六进制的颜色[hexadecimal RGB values](https://en.wikipedia.org/wiki/Web_colors#Hex_triplet)也可以用来表示颜色：`label = tk.Label(text="Hello, Tkinter", background="#34A2FE")`
	
- 可以通过设置前景以及后景，宽度和高度调整Label：
	- 因为Tkiner用的是字符单位（**text units**）。水平和宽度的单位都是数字0的测量值（所以你知道为什么10\*10不是一个正方形了吧）。
		- 通过字符宽度测量单位意味着小部件的大小是相对于用户计算机上的默认字体的。这可以确保文本正确地适合标签和按钮，无论应用程序在何处运行。

```python
label = tk.Label(
    text="Hello, Tkinter",
    fg="white",
    bg="black",
    width=10,
    height=10
)
```
![](https://files.realpython.com/media/17_5_tk_label.ce0f9500e539.jpg)

### Button

- 用来做成可点击的按钮。
- 可以配置成按下去后调用一个函数。
- Button和Label有很多的相似之处，某种意义上，Button就是一个可供点击的Label--> 也就是说Label的好多参数，Button同样可以使用。

```python
button = tk.Button(
    text="Click me!",
    width=25,
    height=5,
    bg="blue",
    fg="yellow",
)
```
效果图：
![](https://files.realpython.com/media/17_5_tk_button.ce3900b68c42.jpg)

### Entry

- 给用户提供输入，但是只能显示一行
- 最重要的是如何从用户处获得输入，主要有以下三种方式：
	1. **Retrieving text** with `.get()`
	2. **Deleting text** with `.delete()`
	3. **Inserting text** with `.insert()`
```python
window = tk.Tk()
label = tk.Label(text="Name")
entry = tk.Entry()
label.pack()
entry.pack()
```

仅仅是上面的代码，并不能获取用户的输入。因为用户的输入并没有发送给程序。可以通过以下方法获取：`name = entry.get()`
- delete方法和字符串分割的用法类似：
	- `entry.delete(0)`:删除第一个字符
	- `entry.delete(0, 4)`:删除0-4这五个字符
	- `entry.delete(0, tk.END)`：删除所有字符串

- Insert方法是插入字符串：
	- `entry.insert(0, "Python")`:0表示插入位置

### Text

- Text提供给用户进行输入，它可以提供多行输入
- 可以认为是扩展版的Entry
- 几个常用的方法：
	1. **Retrieve text** with `.get()`
	2. **Delete text** with `.delete()`
	3. **Insert text** with `.insert()`
- Text的使用方法与以上几个类似：
```Python
window = tk.Tk()

text_box = tk.Text()

text_box.pack()
```

- get方法：需要至少一个参数。
	- `text_box.get("1.0")`:一个参数的话，只返回一个字符
	- `text_box.get("2.0", "2.5")`:
		- 2.0：2表示第二行，0表示第一个字符开始
		- 2.5: 2表示第二行，5表示第五个字符
	- `text_box.get("1.0", tk.END)`: 什么意思显而易见

- delete方法用法与get类似，只是删除文字。但是删除后，该行变成了`\n`。我们可以用`text_box.delete("1.0")`删除这个新行字符。
	- `text_box.delete("1.0")`
	- `text_box.delete("1.0", "1.4")`
	- `text_box.delete("1.0", tk.END)`: 清空文本框

- Insert方法：
	- `.insert("<line>.<column>")`
	- `text_box.insert("1.0", "Hello")`: 在首行插入字符
	- `text_box.insert("2.0", "World")`:紧接着第一行尾部插入。如果第一行没有换行符，那么就是紧接着字符后插入。
	- `text_box.insert("2.0", "\nWorld")`: 换行插入
	- `text_box.insert(tk.END, "Put me at the end!")`:  在文本框末尾追加字符串。

There are several others, including widgets for checkboxes, radio buttons, scroll bars, and progress bars. For more information on all of the available widgets, see the Additional Widgets list in the [Additional Resources](https://realpython.com/python-gui-tkinter/#additional-resources) section.


### Frame

- Frame是用来组织页面上小部件（widgets）的布局的
- Frame是给其他部件提供容器的最好选择
```python
import tkinter as tk

window = tk.Tk()
frame = tk.Frame()
frame.pack()

window.mainloop()
```

可以通过制定部件的master属性，来将一个部件赋给frame。
```python
frame = tk.Frame()
label = tk.Label(master=frame)
```

为了了解具体的工作情况，可以运行测试以下代码：
```python
import tkinter as tk

window = tk.Tk()

frame_a = tk.Frame()
frame_b = tk.Frame()

label_a = tk.Label(master=frame_a, text="I'm in Frame A")
label_a.pack()

label_b = tk.Label(master=frame_b, text="I'm in Frame B")
label_b.pack()

#如果交换下面两行代码的顺序，Frame顺序也会变化
frame_a.pack() 
frame_b.pack()

window.mainloop()
```

运行结果大概是下面这个样子：

![](https://files.realpython.com/media/17_5_tk_two_frames_win10.457151c8c834.jpg)

- `Label`, `Button`, `Entry`, 和 `Text`在实例化后都有master属性。

**Note:** If you omit the `master` argument when creating a new widget instance, then it’ll be placed inside of the top-level window by default.

#### 用Reliefs调整Frame的外观：

- **`tk.FLAT`:** Has no border effect (the default value)
- **`tk.SUNKEN`:** Creates a sunken effect
- **`tk.RAISED`:** Creates a raised effect
- **`tk.GROOVE`:** Creates a grooved border effect
- **`tk.RIDGE`:** Creates a ridged effect

以下为五个不同效果的Frame：
```python
import tkinter as tk

border_effects = {
    "flat": tk.FLAT,
    "sunken": tk.SUNKEN,
    "raised": tk.RAISED,
    "groove": tk.GROOVE,
    "ridge": tk.RIDGE,
}

window = tk.Tk()

for relief_name, relief in border_effects.items():
    frame = tk.Frame(master=window, relief=relief, borderwidth=5)
    frame.pack(side=tk.LEFT)
    label = tk.Label(master=frame, text=relief_name)
    label.pack()

window.mainloop()
```
![](https://files.realpython.com/media/17_5_tk_frame_reliefs_win10.31d7bc5f4fe6.jpg)

- `borderwidth`: 表示宽度，单位为像素点，至少大于1

## 命名约定  Understanding Widget Naming Conventions

- 如果标签小部件用于显示用户名，那么您可以将该小部件命名为 label_user_name。用于收集用户年龄的 Entry 小部件可能称为entry_age。
- 有时候不需要给部件指定变量的时候，可以在其定义后面直接加上`.pack()`：`tk.Label(text="Hello, Tkinter").pack()`
- 为了使命名的长度降低，可以使用以下缩写：

|Widget Class|Variable Name Prefix|Example|
|---|---|---|
|`Label`|`lbl`|`lbl_name`|
|`Button`|`btn`|`btn_submit`|
|`Entry`|`ent`|`ent_age`|
|`Text`|`txt`|`txt_notes`|
|`Frame`|`frm`|`frm_address`|

## 布局的控制管理 Controlling Layout With Geometry Managers

- 一共有三种几何管理器（Geometry Managers）：
	- `.pack()`
	- `.place()`
	- `.grid()`

- Each window or Frame in your application can use only one geometry manager. However, different frames can use different geometry managers, even if they’re assigned to a frame or window using another geometry manager.

###  .pack()

- 利用packing algorithm布置，有两个优先的步骤：
	1. 创建一个满足部件的矩形区域（宽度或者高度适合）：Compute a rectangular area called a **parcel** that’s just tall (or wide) enough to hold the widget and fills the remaining width (or height) in the window with blank space.
	2. 部件优先居中：Center the widget in the parcel unless a different location is specified.
```python
import tkinter as tk

window = tk.Tk()

frame1 = tk.Frame(master=window, width=100, height=100, bg="red")
frame1.pack()

frame2 = tk.Frame(master=window, width=50, height=50, bg="yellow")
frame2.pack()

frame3 = tk.Frame(master=window, width=25, height=25, bg="blue")
frame3.pack()

window.mainloop()
```

效果如下：
![](https://files.realpython.com/media/17_6_tk_pack_vertical_win10.2c0e13c90511.jpg)

- pack()函数可以设置一个方向填满fill：
```python
import tkinter as tk

window = tk.Tk()

frame1 = tk.Frame(master=window, height=100, bg="red")
frame1.pack(fill=tk.X)

frame2 = tk.Frame(master=window, height=50, bg="yellow")
frame2.pack(fill=tk.X)

frame3 = tk.Frame(master=window, height=25, bg="blue")
frame3.pack(fill=tk.X)

window.mainloop()
```

效果如下：
![](https://files.realpython.com/media/17_6_tk_pack_vertical_full_width_win10.ffff0f85671e.jpg)

- **side**关键字指定了小部件应该放置顺序（从左往右？从上往下之类的）：
	- `tk.TOP`：默认是从上往下
	- `tk.BOTTOM`
	- `tk.LEFT`
	- `tk.RIGHT`

```python
import tkinter as tk

window = tk.Tk()

frame1 = tk.Frame(master=window, width=200, height=100, bg="red")
frame1.pack(fill=tk.Y, side=tk.LEFT)

frame2 = tk.Frame(master=window, width=100, bg="yellow")
frame2.pack(fill=tk.Y, side=tk.LEFT)

frame3 = tk.Frame(master=window, width=50, bg="blue")
frame3.pack(fill=tk.Y, side=tk.LEFT)

window.mainloop()
```

可以设置`fill = tk.both`即双向填满:
```python
import tkinter as tk

window = tk.Tk()

frame1 = tk.Frame(master=window, width=200, height=100, bg="red")
frame1.pack(fill=tk.BOTH, side=tk.LEFT, expand=True)

frame2 = tk.Frame(master=window, width=100, bg="yellow")
frame2.pack(fill=tk.BOTH, side=tk.LEFT, expand=True)

frame3 = tk.Frame(master=window, width=50, bg="blue")
frame3.pack(fill=tk.BOTH, side=tk.LEFT, expand=True)

window.mainloop()
```

下面是效果图：

![](https://files.realpython.com/media/tk_full_responsive.57f1ff6e53ab.gif)


### .place()方法

- 精确控制部件的位置
- 需要提供x和y两个参数控制
- 控制的单位为像素，而非字符单位
- 初始的位置（0,0）为窗口或者frame的左上角

```python
import tkinter as tk

window = tk.Tk()

frame = tk.Frame(master=window, width=150, height=150)
frame.pack()

label1 = tk.Label(master=frame, text="I'm at (0, 0)", bg="red")
label1.place(x=0, y=0)

label2 = tk.Label(master=frame, text="I'm at (75, 75)", bg="yellow")
label2.place(x=75, y=75)

window.mainloop()
```

效果如下：
![](https://files.realpython.com/media/17_6_tk_place_win10.676b862a7edd.jpg)

- **两个主要的缺点**：
	1. 布局难管理：Layout can be difficult to manage with `.place()`. This is especially true if your application has lots of widgets.
	2. 布局不会随着窗口大小变化而调整：Layouts created with `.place()` aren’t responsive. They don’t change as the window is resized.
## .grid()方法

- 将窗口以及框架划分为rows和columns，行列开始的坐标均为1
- 指定部件位置时，需要传入行列坐标

```python
import tkinter as tk

window = tk.Tk()

for i in range(3):
    for j in range(3):
        frame = tk.Frame(
            master=window,
            relief=tk.RAISED,
            borderwidth=1
        )
# Each frame is attached to `window` with the `.grid()` geometry manager:
        frame.grid(row=i, column=j)
        label = tk.Label(master=frame, text=f"Row {i}\nColumn {j}")
# Each `label` is attached to its master `Frame` with `.pack()`
        label.pack()

window.mainloop()
```

效果如下：
![](https://files.realpython.com/media/17_6_tk_grid_win10.57eb680e5e6e.jpg)

#### 行列之间间距的调整：
	1. **`padx`** adds padding in the horizontal direction.
	2. **`pady`** adds padding in the vertical direction.

```python
import tkinter as tk

window = tk.Tk()

for i in range(3):
    for j in range(3):
        frame = tk.Frame(
            master=window,
            relief=tk.RAISED,
            borderwidth=1
        )
        frame.grid(row=i, column=j, padx=5, pady=5)
        label = tk.Label(master=frame, text=f"Row {i}\nColumn {j}")
        label.pack()

window.mainloop()
```


效果如下：
![](https://robocrop.realpython.net/?url=https%3A//files.realpython.com/media/17_6_tk_grid_with_ext_padding_win10.20856fb630e9.jpg&w=720&sig=00abe2a790a6bc37e584b6696a7965631692e245)

#### unpack()方法可以用同样的方法调整间距，在此不做赘述。
```python
import tkinter as tk

window = tk.Tk()

for i in range(3):
    for j in range(3):
        frame = tk.Frame(
            master=window,
            relief=tk.RAISED,
            borderwidth=1
        )
        frame.grid(row=i, column=j, padx=5, pady=5)
        label = tk.Label(master=frame, text=f"Row {i}\nColumn {j}")
        label.pack(padx=5, pady=5)

window.mainloop()
```


#### 让部件的大小随着窗口的调整而调整：

- By using `.columnconfigure()` and `.rowconfigure()` on the `window` object, you can adjust how the rows and columns of the grid grow as the window is resized.
-  `.columnconfigure()` and `.rowconfigure()` 需要接受三个参数：
	1. **Index:** The index of the grid column or row that you want to configure or a list of indices to configure multiple rows or columns at the same time
	2. **Weight:** A keyword argument called `weight` that determines how the column or row should respond to window resizing, relative to the other columns and rows. 默认为0，即不变化。
	3. **Minimum Size:** A keyword argument called `minsize` that sets the minimum size of the row height or column width in pixels

```python
import tkinter as tk

window = tk.Tk()

for i in range(3):
    window.columnconfigure(i, weight=1, minsize=75)
    window.rowconfigure(i, weight=1, minsize=50)

    for j in range(0, 3):
        frame = tk.Frame(
            master=window,
            relief=tk.RAISED,
            borderwidth=1
        )
        frame.grid(row=i, column=j, padx=5, pady=5)
        label = tk.Label(master=frame, text=f"Row {i}\nColumn {j}")
        label.pack(padx=5, pady=5)

window.mainloop()
```
窗口设置有最小值是因为需要保证label的字可以被看见。

![](https://files.realpython.com/media/tk_grid_responsive.02edef27aff4.gif)


#### 选择对齐的方式

- 默认所有的部件是居中的, 参考下面两行一列的label
```python
import tkinter as tk

window = tk.Tk()
window.columnconfigure(0, minsize=250)
window.rowconfigure([0, 1], minsize=100)

label1 = tk.Label(text="A")
label1.grid(row=0, column=0)

label2 = tk.Label(text="B")
label2.grid(row=1, column=0)

window.mainloop()
```

![](https://files.realpython.com/media/17_6_tk_grid_col_and_row_size_win10.c6e03e9483bd.jpg)

- 可以通过`sticky`参数调整。
	- **`"n"` or `"N"`** to align to the top-center part of the cell
	- **`"e"` or `"E"`** to align to the right-center side of the cell
	- **`"s"` or `"S"`** to align to the bottom-center part of the cell
	- **`"w"` or `"W"`** to align to the left-center side of the cell

```python
import tkinter as tk

window = tk.Tk()
window.columnconfigure(0, minsize=250)
window.rowconfigure([0, 1], minsize=100)

label1 = tk.Label(text="A")
label1.grid(row=0, column=0, sticky="ne")

label2 = tk.Label(text="B")
label2.grid(row=1, column=0, sticky="sw")

window.mainloop()
```

![](https://robocrop.realpython.net/?url=https%3A//files.realpython.com/media/17_6_tk_grid_sticky_corners_win10.67d522344ba9.jpg&w=689&sig=be0af58d752d009522bbd8299079cba76006be65)

- In order to fill the grid, you can specify `"ns"` to force the widget to fill the cell in the vertical direction, or `"ew"` to fill the cell in the horizontal direction. To fill the entire cell, set `sticky` to `"nsew"`. The following example illustrates each of these options:
```python
import tkinter as tk

window = tk.Tk()

window.rowconfigure(0, minsize=50)
window.columnconfigure([0, 1, 2, 3], minsize=50)

label1 = tk.Label(text="1", bg="black", fg="white")
label2 = tk.Label(text="2", bg="black", fg="white")
label3 = tk.Label(text="3", bg="black", fg="white")
label4 = tk.Label(text="4", bg="black", fg="white")

label1.grid(row=0, column=0)
label2.grid(row=0, column=1, sticky="ew")
label3.grid(row=0, column=2, sticky="ns")
label4.grid(row=0, column=3, sticky="nsew")

window.mainloop()
```

![](https://files.realpython.com/media/17_6_tk_grid_sticky_fill_win10.beea5d30319e.jpg)

- sticky的填充形式与pack类似：

|`.grid()`|`.pack()`|
|---|---|
|`sticky="ns"`|`fill=tk.Y`|
|`sticky="ew"`|`fill=tk.X`|
|`sticky="nsew"`|`fill=tk.BOTH`|
- <u>grid方法比pack()方法易于理解，且比place()方法复杂，因此应当优先使用。</u>

**Note:** `.grid()` offers much more flexibility than you’ve seen here. For example, you can configure cells to span multiple rows and columns. For more information, check out the [Grid Geometry Manager section](https://tkdocs.com/tutorial/grid.html) of the [TkDocs tutorial](https://tkdocs.com/tutorial/index.html).

# 让应用程序可以交互  Making Your Applications Interactive

- 事件（event）：指发生在event loop中的一些会产生一些行为的动作，例如鼠标被按下等等。
- When an event occurs, an event object is emitted, which means that an instance of a class representing the event is created.
- 需要用户写event handler的程序来处理这些事件。
- 调用`window.mainloop()`的时候，就会自动开启事件循环（event loop）.
- 事件循环的时候，程序会自动check是否有其他的事件（event）发生。类似于下面伪代码所表现的：
```python
events = []

# Create an event handler
def handle_keypress(event):
    """Print the character associated to the key pressed"""
    print(event.char)

while True:
    if events == []:
        continue

    event = events[0]

    # If event is a keypress event object
    if event.type == "keypress":
        # Call the keypress event handler
        handle_keypress(event)
```


## bind方法：将event handler和event绑定

- 程序是不知道哪个事件和哪个处理是对应的，所以需要进行绑定

以下代码将\<key\>事件和handle_keypress绑定在了一起，按下什么，都会在终端回显。
```python
import tkinter as tk

window = tk.Tk()

def handle_keypress(event):
    """Print the character associated to the key pressed"""
    print(event.char)

# Bind keypress event to handle_keypress()
window.bind("<Key>", handle_keypress)

window.mainloop()
```

- bind一般至少需要两个参数：
	1. An **event** that’s represented by a string of the form `"<event_name>"`, where `event_name` can be any of Tkinter’s events
	2. An **event handler** that’s the name of the function to be called whenever the event occurs

- bind会被绑定到调用的部件上，换言之：`event_name.bind(Action,"handler_function")`

```python
def handle_click(event):
    print("The button was clicked!")

button = tk.Button(text="Click me!")

button.bind("<Button-1>", handle_click)
```

以上代码会窗口被左键的时候，打印相关内容。对于鼠标，常见的操作还有：
- `"<Button-1>"` ：左键
- `"<Button-2>"` ：中键
- `"<Button-3>"` ：右键

**Note:** For a list of commonly used events, see the [Event types](https://web.archive.org/web/20190512164300/http://infohost.nmt.edu/tcc/help/pubs/tkinter/web/event-types.html) section of the [Tkinter 8.5 reference](https://web.archive.org/web/20190524140835/https://infohost.nmt.edu/tcc/help/pubs/tkinter/web/index.html).

## 运用命令 Using command

- Every `Button` widget has a `command` attribute that you can assign to a function. Whenever the button is pressed, the function is executed.
- 本质就是把事件处理函数当做command传给Button对象

```python
import tkinter as tk

def increase():
    value = int(lbl_value["text"])
    lbl_value["text"] = f"{value + 1}"

def decrease():
    value = int(lbl_value["text"])
    lbl_value["text"] = f"{value - 1}"

window = tk.Tk()

window.rowconfigure(0, minsize=50, weight=1)
window.columnconfigure([0, 1, 2], minsize=50, weight=1)

btn_decrease = tk.Button(master=window, text="-", command=decrease)
btn_decrease.grid(row=0, column=0, sticky="nsew")

lbl_value = tk.Label(master=window, text="0")
lbl_value.grid(row=0, column=1)

btn_increase = tk.Button(master=window, text="+", command=increase)
btn_increase.grid(row=0, column=2, sticky="nsew")

window.mainloop()
```

效果如下：
![](https://files.realpython.com/media/tk_counter_app.dccc1ac46c32.gif)

- command后面可以接一个函数列表function_list[]，例如：
```python
drop_btn = tk.Button(frm_buttons,text="Drop",bg="blue",fg="yellow",command=lambda: [animation(gif_lbl,drop_page_w,current_frame=0), drop_name(name_lbl)])
```


# 华摄氏度和摄氏度转换

```python
import tkinter as tk

def fahrenheit_to_celsius():
    """Convert the value for Fahrenheit to Celsius and insert the
    result into lbl_result.
    """
    fahrenheit = ent_temperature.get()
    celsius = (5 / 9) * (float(fahrenheit) - 32)
    lbl_result["text"] = f"{round(celsius, 2)} \N{DEGREE CELSIUS}"

# Set up the window
window = tk.Tk()
window.title("Temperature Converter")
window.resizable(width=False, height=False)

# Create the Fahrenheit entry frame with an Entry
# widget and label in it
frm_entry = tk.Frame(master=window)
ent_temperature = tk.Entry(master=frm_entry, width=10)
lbl_temp = tk.Label(master=frm_entry, text="\N{DEGREE FAHRENHEIT}")

# Layout the temperature Entry and Label in frm_entry
# using the .grid() geometry manager
ent_temperature.grid(row=0, column=0, sticky="e")
lbl_temp.grid(row=0, column=1, sticky="w")

# Create the conversion Button and result display Label
btn_convert = tk.Button(
    master=window,
    text="\N{RIGHTWARDS BLACK ARROW}",
    command=fahrenheit_to_celsius
)
lbl_result = tk.Label(master=window, text="\N{DEGREE CELSIUS}")

# Set up the layout using the .grid() geometry manager
frm_entry.grid(row=0, column=0, padx=10)
btn_convert.grid(row=0, column=1, pady=10)
lbl_result.grid(row=0, column=2, padx=10)

# Run the application
window.mainloop()
```
![](https://files.realpython.com/media/17_8_tk_temp_converter_win10.8e1ebad492b9.jpg)

# 写一个文本编辑器

```python
import tkinter as tk
from tkinter.filedialog import askopenfilename, asksaveasfilename

def open_file():
    """Open a file for editing."""
    filepath = askopenfilename(
        filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")]
    )
    if not filepath:
        return
    txt_edit.delete("1.0", tk.END)
    with open(filepath, mode="r", encoding="utf-8") as input_file:
        text = input_file.read()
        txt_edit.insert(tk.END, text)
    window.title(f"Simple Text Editor - {filepath}")

def save_file():
    """Save the current file as a new file."""
    filepath = asksaveasfilename(
        defaultextension=".txt",
        filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")],
    )
    if not filepath:
        return
    with open(filepath, mode="w", encoding="utf-8") as output_file:
        text = txt_edit.get("1.0", tk.END)
        output_file.write(text)
    window.title(f"Simple Text Editor - {filepath}")

window = tk.Tk()
window.title("Simple Text Editor")

window.rowconfigure(0, minsize=800, weight=1)
window.columnconfigure(1, minsize=800, weight=1)

txt_edit = tk.Text(window)
frm_buttons = tk.Frame(window, relief=tk.RAISED, bd=2)
btn_open = tk.Button(frm_buttons, text="Open", command=open_file)
btn_save = tk.Button(frm_buttons, text="Save As...", command=save_file)

btn_open.grid(row=0, column=0, sticky="ew", padx=5, pady=5)
btn_save.grid(row=1, column=0, sticky="ew", padx=5)

frm_buttons.grid(row=0, column=0, sticky="ns")
txt_edit.grid(row=0, column=1, sticky="nsew")

window.mainloop()
```

![](https://files.realpython.com/media/17_9_tk_text_editor_win10.9182347f4b5d.jpg)



# 如何用Tkinter显示Gif

参考：[Displaying Gifs in Tkinter - Python](https://devhubcommunity.hashnode.dev/displaying-gifs-in-tkinter-python)

- gif: a collection of frames(images) that are shown in a sequence, in a loop, thus creating an animation effect.

## s1 Import required packages

```python
import tkinter as tk
from PIL import Image
```

## s2 Create the main application window and run the event loop

```python
root = tk.Tk()
root.title("Displaing Gif")

root.mainloop()
```

## s3 Add labels and buttons

In `gif_label` gif will be displayed. And we have a **start** and **stop** button to control the gif.
```python
gif_label = tk.Label(root, image="")
gif_label.pack()

start = tk.Button(root, text="Start", command = lambda: animation(current_frame = 0))
start.pack()

stop = tk.Button(root, text="Stop", commnad = stop_animation)
stop.pack()

```

## S4  Store Gif's path in the variable and open it using the pillow module.

- Get the number of frames in the Gif and then create photoimage object for each frame and store them in a list.
- 
- `format` parameter in the photoimage class is required to read the frames of the gif.
```python
file = "gif_file.gif"
info = Image.open(file)
frames = info.n_frames # number of frames

photoimage_objects = []
for i in range(frames):
    obj = tk.PhotoImage(file = file, format = f"gif -index {i}")
    photoimage_objects.append(obj)
```

## S5 Create functions: animation and stop_animation to start and stop the gif respectively

```python
def animation(current_frame=0):
    global loop
    image = photoimage_objects[current_frame]

    gif_label.configure(image = image)
    current_frame = current_frame + 1

    if current_frame == frames:
        current_frame = 0 # reset the current_frame to 0 when end is reached

    loop = root.after(50, lambda: animation(current_frame))
```

The above `animation` function takes `current_frame` as an argument, which indicates the frame number that is going to be displayed.  
So to display gif we have to start showing frames from the 0th index.

And to continuously update the frame we have to keep calling the function in a loop so we used `root.after()` which calls the function after every 50ms

## S6 Create stop_animation function

```python
def stop_animation():
    root.after_cancel(loop)
```

`root.after_cancel(loop)` cancels the scheduled function which has an after_id = loop.

That's why we declared `loop = None`, outside the function so that it can be used in both start and stop_animation.

以下为完整代码：
```python
import tkinter as tk
from PIL import Image

root = tk.Tk()
root.title("Displaing Gif")

file = "gif_file.gif"
info = Image.open(file)

frames = info.n_frames  # number of frames

photoimage_objects = []
for i in range(frames):
    obj = tk.PhotoImage(file=file, format=f"gif -index {i}")
    photoimage_objects.append(obj)


def animation(current_frame=0):
    global loop
    image = photoimage_objects[current_frame]

    gif_label.configure(image=image)
    current_frame = current_frame + 1

    if current_frame == frames:
        current_frame = 0

    loop = root.after(50, lambda: animation(current_frame))


def stop_animation():
    root.after_cancel(loop)


gif_label = tk.Label(root, image="")
gif_label.pack()

start = tk.Button(root, text="Start", command=lambda: animation(current_frame=0))
start.pack()

stop = tk.Button(root, text="Stop", command=stop_animation)
stop.pack()

root.mainloop()

```

# **Tkinter References**

Here are some official resources to check out:

- The [official Python Tkinter reference documentation](https://docs.python.org/3/library/tkinter.html) covers Python’s Tkinter module in moderate depth. It’s written for more advanced Python developers and isn’t the best resource for beginners.
- [Tkinter 8.5 reference: a GUI for Python](https://web.archive.org/web/20190524140835/https://infohost.nmt.edu/tcc/help/pubs/tkinter/web/index.html) is an extensive reference covering the majority of the Tkinter module. It’s exhaustive, but it’s written in the reference style without commentary or examples.
- The [Tk Commands](https://www.tcl.tk/man/tcl/TkCmd/contents.htm) reference is the definitive guide to commands in the Tk library. It’s written for the Tcl language, but it answers a lot of questions about why things work the way they do in Tkinter.
