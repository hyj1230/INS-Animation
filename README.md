# 快速上手
1. 创建一个类（以按钮为例）
```
class Button:
    def __init__(self):
        self.w, self.h = 200, 100
```

2. 添加动画内容
```
class Button:
    def __init__(self):
        self.w, self.h = 200, 100
        self.hover_transition = TransitionGroup()
        self.hover_transition.add_transition([
            transition((self, 'w', self.w * 1.5), '0.1s', 'ease-in-out', '0s')
        ])
```

3. 动画开始后在主循环里进行更新
```
button.hover_transition.start()  # 动画开始播放
while True:
    # 此处省略
    button.hover_transition.update()
```

# API 文档
## `easing_function` 缓动函数
`linear`: 线性缓动函数  
`ease`, `ease_in`, `ease_in_out`, `ease_out`: 非线性缓动函数  
`CubicBezier()`: 自定义贝塞尔曲线缓动函数

## `transition` 过渡动画
**`transition()`:**
> 创建一个过渡动画
>
> 参数:  
> **`transition_property`: 元组类型**  
> （被执行动画的类, 被执行动画的类变量名, 动画执行后该变量的值)
>
> 
> **`transition_duration`: 动画持续时间**  
> 默认值: `'0s'`  
> 格式：
> 1. 整数、浮点数（以秒为单位）
> 2. 字符串类型，数字加单位，如 `'0.1s'`, `'20ms'`
>
> **`transition_timing_function`: 动画使用的缓动函数**  
> 默认值: ease  
> 格式：
> 1. 字符串格式的内置缓动函数，包括`'linear'`, `'ease'`, `'ease-in'`, `'ease-out'`, `'ease-in-out'`
> 2. 字符串形式的自定义缓动函数，如 `'cubic-bezier(.17, .67, .83, .67)'`
> 3. 上文 `easing_function` 的格式
>
> **`transition_delay`: 动画开始的延迟**  
> 默认值: '0s'
> 格式：同 `transition_duration`
> 
> **`lerp_function`: 插值用的函数（非特殊情况无需变动）**  
> 默认值: `lerp`（数字类型的插值）
>
> **返回值：`Transition` 类**

**`Transition` 类：**  
> 用于单个动画的类
> 
> `play`: True 或 False，代表动画是否在播放中  
> `update()`: 动画更新，否则无法播放  
> `start()`: 开始播放动画  
> `stop()`: 强制停止动画播放

**`TransitionGroup` 类：**  
> 动画组，用于同时执行多个动画
> 
> `play`: True 或 False，代表动画是否在播放中  
> `add_transition(_transition)`: 添加动画  
> > `_transition` 格式: 
> > 1. 单个 `Transition` 类
> > 2. 包含 `Transition` 类的元组和列表
> 
> `update()`: 动画更新，否则无法播放  
> `start()`: 开始播放动画  
> `stop()`: 强制停止动画播放
