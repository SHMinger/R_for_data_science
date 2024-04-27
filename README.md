<img src="http://www.shminger.cn:3380/images/2024/04/21/202404211306819.png" style="zoom:25%;" />

# R数据科学

## 第一章、使用ggplot2进行数据可视化

### 0 准备工作

```R
install.package("tidyverse")
library(tidyverse)		# R包只需要安装一次，但每次运行都需提前加载

# package::function()使用包中的特定函数
ggplot2::ggplot()

ggplot2::mpg		# package::function()命令指出函数的来源,输出同mpg
# 注：①在加载tidyverse前先运行一下内容，就没有提示了。
options(tidyverse.quiet = TRUE)
```

<table>
	<tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/Fig.1-2-mpg.png" alt="Fig.0.1.2" style="zoom:50%;" />
      <center>Fig.0.1.2</center></td>
  </tr>
</table>



### 1 mpg数据框及绘图

#### 1.3 图形属性映射

```R
# ggplot2绘图
mpg    # 38种车型及观测数据, Fuel economy data from 1999 to 2008 for 38 popular models of cars
?mpg		# 输出同ggplot2::mpg
# 绘图模板：
ggplot(data = <DATA>) +
	<GEOM_FUNCTION>(mapping = aes(<MAPPINGS>))
# Fig.1.3.1 
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy))

# 1.3图形属性映射
# size参数控住图形大小的图形属性
# Fig.1.3.2
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, size = class))  
# >Warning message: Using size for a discrete variable is not advised. 

# alpha参数为控制透明度的图形属性
# Fig.1.3.3
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, alpha = class))
# Warning message: Using alpha for a discrete variable is not advised. 

# shape参数，ggplot2()函数只能同时显示6种形状
# Fig.1.3.4
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, shape = class))
# >Warning messages:
# 1: The shape palette can deal with a maximum of 6 discrete values because more than 6
# becomes difficult to discriminate; you have 7. Consider specifying shapes manually if you must have them. 
# 2: Removed 62 rows containing missing values (geom_point). 

# color参数
# Fig.1.3.5
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class))
# Fig.1.3.7
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy), color = "blue")		
# Fig.1.3.7
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = "blue"))		# 图形颜色不能变为蓝色,此时color代表一个参数
# Fig.1.3.8
ggplot(data = mpg) + 
	geom_point(mapping = aes(x = displ, y = hwy), shape = 0, size = 3, color = "blue")

```

<table>
	<tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211149886.png" alt="Fig.1.3.1" style="zoom:50%;" />
      <center>Fig.1.3.1</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211151690.png" alt="Fig.1.3.2" style="zoom:50%" />
      <center>Fig.1.3.2</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211153272.png" alt="Fig.1.3.3" style="zoom:50%" />
      <center>Fig.1.3.3</center></td>
  </tr>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211154748.png" alt="Fig.1.3.4" style="zoom:50%;" />
      <center>Fig.1.3.4</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211156496.png" alt="Fig.1.3.5" style="zoom:50%;" />
      <center>Fig.1.3.5</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211157431.png" alt="Fig.1.3.6" style="zoom:50%;" />
      <center>Fig.1.3.6</center></td>
  </tr>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211158649.png" alt="Fig.1.3.7" style="zoom:50%;" />
      <center>Fig.1.3.7</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211159378.png" alt="Fig.1.3.8" style="zoom:50%" />
      <center>Fig.1.3.8</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202003074.png" alt="Fig.1.3.9" style="zoom:50%" />
      <center>Fig.1.3.9 用数值进行标识的R的25种内置形状</center></td>
  </tr>
</table>



#### 1.5 分面

```R
# 1.5 分面：facet_wrap()，facet_grid()
#  facet_wrap()对图形进行分面
# Fig.1.5.1
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_wrap(~ class, nrow = 2)		# face_wrap()函数的变量为离散型数据

# facet_grid()含有两个公式(数据结构)，公式间用“~”隔开
# Fig.1.5.2
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = drv, y = cyl))
# Fig.1.5.3
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ cyl)		# 输出为3行4列

# Fig.1.5.4
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(. ~ cyl)		# 输出为4列,只输出上图的所有列，cyl代表列

# Fig.1.5.5
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  facet_grid(drv ~ .)		# 输出为3行，只输出上图所有的行，drv代表行

# Fig.1.5.6
p1 <- ggplot(data = mpg, mapping = aes(displ, hwy)) +
      geom_point(size = 2.5) +
      geom_smooth(se = F, size = 1.5)
p2 <- ggplot(data = mpg, mapping = aes(displ, hwy)) +
      geom_point(size = 2.5) +
      geom_smooth(se = F, size = 1.5, mapping = aes(group = drv))
p3 <- ggplot(data = mpg, mapping = aes(displ, hwy, color = drv)) +
      geom_point(size = 2.5) +
      geom_smooth(se = F, size = 1.5, mapping = aes(group = drv, color = drv))
p4 <- ggplot(data = mpg, mapping = aes(displ, hwy)) +
      geom_point(size = 2.5, mapping = aes(color = drv)) +
      geom_smooth(se = F, size = 1.5)
p5 <- ggplot(data = mpg, mapping = aes(displ, hwy)) +
      geom_point(size = 2.5, mapping = aes(color = drv)) +
      geom_smooth(se = F, size = 1.5, mapping = aes(group = drv, linetype = drv))
p6 <- ggplot(data = mpg, mapping = aes(displ, hwy)) +
      geom_point(size = 2.5, mapping = aes(color = drv))
# method 1
suppressWarnings(library(gridExtra))
grid.arrange(p1, p2, p3, p4, p5, p6, ncol= 2, nrow = 3)
# method 2
suppressWarnings(library(cowplot))
plot_grid(p1, p2, p3, p4, p5, p6, nrow=3, ncol=2, labels = c("A","B","C","D","E","F"))
#method 3
#suppressWarnings(library(patchwork))
library(patchwork)
p1 + p2 + p3 + p4 + p5 + p6 + plot_layout(nrow = 3) + plot_annotation(tag_levels = 'A')
```

<table>
	<tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211205359.png" alt="Fig.1.5.1" style="zoom:50%;" />
      <center>Fig.1.5.1</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211207601.png" alt="Fig.1.5.2" style="zoom:50%" />
      <center>Fig.1.5.2</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211207224.png" alt="Fig.1.5.3" style="zoom:50%" />
      <center>Fig.1.5.3</center></td>
  </tr>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211208739.png" alt="Fig.1.5.4" style="zoom:50%;" />
      <center>Fig.1.5.4</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211209885.png" alt="Fig.1.5.5" style="zoom:50%;" />
      <center>Fig.1.5.5</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211217708.png" alt="Fig.1.5.6" style="zoom:50%;" />
      <center>Fig.1.5.6</center></td>
  </tr>
</table>



#### 1.6 几何对象

```R
# 1.6 几何对象
# 几何对象是图中用来表示数据的几何图形对象
# Fig.1.6.1
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy)) +
  geom_smooth(mapping = aes(x = displ, y = hwy))		# ggplot()函数中添加多个几何对象函数，对点图进行拟合
# 上式简化
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 		# 全局映射
    geom_point() +
    geom_smooth()		# 默认显示置信区间

# Fig.1.6.2
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 		# 局部映射
    geom_point(mapping = aes(color = class)) +
    geom_smooth()

# Fig.1.6.3
ggplot(data = mpg, mapping = aes(x = displ,y = hwy)) +
      geom_point(mapping = aes(color = class)) +
      geom_smooth(
      	data = filter(mpg, class == "subcompact"),		# ?filter()
      	se = FALSE		# se显示平滑周围的置信区间
      )

# 测试
# Fig.1.6.4
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) +
	geom_point() +
	geom_smooth(se = FALSE)

# geom_smooth()的参数linetype线型，geom_point()的参数有shape参数
# Fig.1.6.5
ggplot(data = mpg) + 
  geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv))

# ggplot2对数据进行分组绘制多个几何对象
# Fig.1.6.6
ggplot(data = mpg) +
	geom_smooth(mapping = aes(x = displ, y = hwy, group = drv))

# Fig.1.6.7
ggplot(data = mpg) + 
  geom_smooth(
    mapping = aes(x = displ, y = hwy, color = drv), 
    show.legend = FALSE		# 不显示图例(legend)
  )

# Fig.1.6.8
ggplot(data = mpg) + 
    geom_point(mapping = aes(x = displ, y = hwy, color = class)) +
    geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv))
```

<table>
	<tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211221509.png" alt="Fig.1.6.1" style="zoom:50%;" />
      <center>Fig.1.6.1</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211222949.png" alt="Fig.1.6.2" style="zoom:50%" />
      <center>Fig.1.6.2</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211223225.png" alt="Fig.1.6.3" style="zoom:50%" />
      <center>Fig.1.6.3</center></td>
  </tr>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211223156.png" alt="Fig.1.6.4" style="zoom:50%;" />
      <center>Fig.1.6.4</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211224487.png" alt="Fig.1.6.5" style="zoom:50%;" />
      <center>Fig.1.6.5</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211224591.png" alt="Fig.1.6.6" style="zoom:50%;" />
      <center>Fig.1.6.6</center></td>
  </tr>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211225615.png" alt="Fig.1.6.7" style="zoom:50%;" />
      <center>Fig.1.6.7</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211226710.png" alt="Fig.1.6.8" style="zoom:50%;" />
      <center>Fig.1.6.8</center></td>
  </tr>
</table>



#### 1.7 统计变换

```R
# 1.7 统计变换: stat算法
# Fig.1.7.1
ggplot(data = diamonds) +
		geom_bar(aes(x = cut))

# Fig.1.7.2
ggplot(data = diamonds) +
		geom_bar(aes(x = color), width = 0.5, na.rm = FALSE)
# 等同：
ggplot(data = diamonds) +
		stat_count(aes(x = cut))

# Fig.1.7.3
demo <- tribble(
		~a,		~b,
		"bar_1", 20,
  	"bar_2", 40,
  	"bar_3", 60,
  	"bar_4", 80,
  	"bar_5", 100
)
ggplot(data=demo) +
		geom_bar(mapping = aes(x = a, y = b), stat = "identity")

# Fig.1.7.4
ggplot(data = diamonds) +
    geom_bar(mapping = aes(x= cut, y = ..prop.., group = 1))		# 按比例显示条形图

# Fig.1.7.5
ggplot(data = diamonds) +
    stat_summary(mapping = aes(x = cut, y= depth),
    		fun.ymin = min,
    		fun.ymax = max,
    		fun.y =median
    )		# 摘要统计量：最大值，最小值，平均值

# Fig.1.7.6
ggplot(data = diamonds) + 
		geom_bar(mapping = aes(x = cut, y = ..prop..))
# Fig.1.7.7
ggplot(data = diamonds) + 
		geom_bar(mapping = aes(x = cut, fill = color, y = ..prop..))
```

<table>
	<tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211228304.png" alt="Fig.1.7.1" style="zoom:50%;" />
      <center>Fig.1.7.1</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211229392.png" alt="Fig.1.7.2" style="zoom:50%" />
      <center>Fig.1.7.2</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211230059.png" alt="Fig.1.7.3" style="zoom:50%" />
      <center>Fig.1.7.3</center></td>
  </tr>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211230516.png" alt="Fig.1.7.4" style="zoom:50%;" />
      <center>Fig.1.7.4</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211231139.png" alt="Fig.1.7.5" style="zoom:50%;" />
      <center>Fig.1.7.5</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211231738.png" alt="Fig.1.7.6" style="zoom:50%;" />
      <center>Fig.1.7.6</center></td>
  </tr>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211232871.png" alt="Fig.1.7.7" style="zoom:50%;" />
      <center>Fig.1.6.7</center></td>
  </tr>
</table>



#### 1.8 位置调整

```R
# 1.8 位置调整
# Fig1.8.1
ggplot(data = diamonds) +
    geom_bar(mapping = aes(x = cut, color = cut))		# 条形图边框颜色
# Fig1.8.2
ggplot(data = diamonds) +
    geom_bar(mapping = aes(x = cut, fill = cut))		# 条形图填充颜色

# Fig.1.8.3
ggplot(data = diamonds) +
    geom_bar(mapping = aes(x = cut, fill = clarity))		# 条形图分块堆叠，由position参数设定的位置调整功能完成

# Fig.1.8.4
ggplot(data = diamonds,
    mapping = aes(x = cut, fill = clarity)) +
    geom_bar(alpha = 1/5, position = "identity")
# Fig.1.8.5
ggplot(data = diamonds,
    mapping = aes(x = cut, color = clarity)) +
    geom_bar(fill = NA, position = "identity")

# Fig.1.8.6
ggplot(data = diamonds) +
    geom_bar(mapping = aes(x = cut, fill = clarity), position = "fill")		# 每组条形堆叠具有相同高度
# Fig.1.8.7
ggplot(data = diamonds) +
    geom_bar(mapping = aes(x = cut, fill = clarity), position = "dodge")		# 每组条形并列排放

# Fig.1.8.8
ggplot(data = mpg) + 
  	geom_point(mapping = aes(x = displ, y = hwy), position = "jitter")		# 对数据点随机扰动
# Fig.1.8.9
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) +
		geom_jiter()

```

<table>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202306527.png" alt="Fig.1.8.1" style="zoom:50%;" />
      <center>Fig.1.8.1</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202308168.png" alt="Fig.1.8.2" style="zoom:50%;" />
      <center>Fig.1.8.2</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202309747.png" alt="Fig.1.8.3" style="zoom:50%;" />
      <center>Fig.1.8.3</center></td>
  </tr>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202315720.png" alt="Fig.1.8.4" style="zoom:50%;" />
      <center>Fig.1.8.4</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202316101.png" alt="Fig.1.8.5" style="zoom:50%;" />
      <center>Fig.1.8.5</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202320086.png" alt="Fig.1.8.6" style="zoom:50%;" />
      <center>Fig.1.8.6</center></td>
  </tr>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202321731.png" alt="Fig.1.8.7" style="zoom:50%;" />
      <center>Fig.1.8.7</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202323337.png" alt="Fig.1.8.8" style="zoom:50%;" />
      <center>Fig.1.8.8</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202328701.png" alt="Fig.1.8.9" style="zoom:50%;" />
      <center>Fig.1.8.9</center></td>
  </tr>
</table>

#### 1.9 坐标系

```R
# 1.9 坐标系
# coord_flip()函数可以交换x轴和y轴
# Fig.1.9.1
ggplot(data = mpg, mapping = aes(x = class, y =hwy)) +
	geom_boxplot()
# Fig.1.9.2
ggplot(data = mpg, mapping = aes(x = class, y =hwy)) +
	geom_boxplot() +	
	coord_flip()

# coord_quickmap()函数可以为地图设置合适的纵横比
# Fig.1.9.3
nz <- map_data("nz")
ggplot(nz, aes(long, lat, group = group)) +
	geom_polygon(fill = "white", color = "black")
# Fig.1.9.4
ggplot(nz, aes(long, lat, group = group)) +
	geom_polygon(fill = "white", color = "black") +
	coord_quickmap()

# coord_polar()函数使用极坐标系
bar <- ggplot(data = diamonds) +
	geom_bar(
  	mapping = aes(x = cut, fill = cut),
  	show.legend = FALSE,
  	width = 1
  ) +
	theme(aspect.ratio = 1) +
	labs(x = NULL, y = NULL)
# Fig.1.9.5
bar + coord_flip()
# Fig.1.9.6
bar + coord_polar()

```

<table>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202333714.png" alt="Fig.1.9.1" style="zoom:50%;" />
      <center>Fig.1.9.1</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202335366.png" alt="Fig.1.9.2" style="zoom:50%;" />
      <center>Fig.1.9.2</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202340296.png" alt="Fig.1.9.3" style="zoom:50%;" />
      <center>Fig.1.9.3</center></td>
  </tr>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202342732.png" alt="Fig.1.9.4" style="zoom:50%;" />
      <center>Fig.1.9.4</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202346025.png" alt="Fig.1.9.5" style="zoom:50%;" />
      <center>Fig.1.9.5</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/20/202404202347247.png" alt="Fig.1.9.6" style="zoom:50%;" />
      <center>Fig.1.9.6</center></td>
  </tr>
</table>

#### 1.10 图形分层语法

```R
# 1.10 图形分层语法
ggplot(data = <DATA>) +
	<GEOM_FUNCTION>(
  	mapping = aes(<MAPPINGS>),
  	stat = <STAT>,
  	position = <POSITION>
  ) +
	<COORDINATE_FUNCTION> +
	<FACET_FUNCTION>
```



### 2 工作流：基础

```R

```





### 3. 使用dplyr进行数据转换

#### 3.1 准备工作

```R
# 3.1 准备工作
library(nycflights13)
library(tidyverse)

# dplyr基础：5个核心函数
# filter()按值筛选观测
# arrange()对行进行重新排序
# select()按名称选取变量
# mutate()使用现有变量的函数创建变量
# summarize()将多个值总结为一个摘要统计量

```

#### 3.2 使用filter()筛选行

```R
# 3.2 使用filter()筛选行
filter(flights, month == 1, day == 1)		# 筛选2013年1月1日的所有航班
jan1 <- filter(flights, month == 1, day == 1)		# 将新的数据库赋值到变量jan1
(dec25 <- filter(flights, month == 12, day == 25))	# 输出结果，同时将新的数据库赋值到变量dec25

# 比较运算符：>, >=, <, <=, !=, ==
# 区别：赋值运算符：=
#有限精度运算，比较浮点数是否相等时，使用near()
near(sqrt(2) ^ 2, 2)
near(1 / 49 * 49, 1)

# 逻辑运算符
# &：与, |：或, !：非
filter(flights, month == 11 | month == 12)		# 2013年11月或12月出发的航班
filter(flights, month == 11 | 12)		# 11 | 12的值为TRUE（1），输出的是1月的航班

nov_dec <- filter(flights, month %in% c(11, 12))

filter(flights, !(arr_delay > 120 | dep_delay >120))		# 延误时间(到达或出发)不多于2小时的航班
filter(flights, arr_delay <= 120, dep_dela <=120)

# 缺失值：NA
is.na(x)		# 判断x是否为缺失值

df <- tibble(x = c(1, NA, 3))		# filter()函数只能筛选出条件为TRUE的行
filter(df, x > 1)
filter(df, is.na(x) | x >1)
```

#### 3.3 使用arrange()排列行

```R
# 3.3 使用arrange()排列行
arrange(flights, year, month, day)		# 改变行的顺序
arrange(flights, desc(arr_delay))		# 使用desc()可以按列进行降序排序

df <- tibble(x = c(5, 2, NA))		# NA总数排在最后,不论正序还是倒序
arrange(df, x)
arrange(df, desc(x))
```

#### 3.4 使用select()选择列

```R
# 3.4 使用select()选择列
select(flights, year, month, day)		# 按名称选择列
select(flights, year:day)		# 按区间选择列
select(flights, -(year:day))	# 按排除区间选择列

# select()函数的辅助函数：
# starts_with("abc"): 匹配已"abc"开头的名称
# ends_with("xyz"): 匹配以"xyz"结尾的名称
# contains("ijk"): 匹配包含“ijk”的名称
# matches("(.)\\1"): 选择匹配正则表达式的那些变量
# num_range("x", 1:3): 匹配x1、x2和x3

# rename()函数重命名变量
rename(flights, tail_num = tailnum)
# select()与everything()函数结合，将变量移到数据框开头
select(flights, time_hour, air_time, everything())
```

#### 3.5 使用mutate()添加新变量

```R
# 3.5 使用mutate()添加新变量
flights_sml <- select(flights,
                     year:day,
                     ends_with("delay"),
                     distance,
                     air_time
                     )
mutate(flights_sml,
      gain = arr_delay - dep_delay,
      speed = distance / air_time * 60
      )
mutate(flights_sml,
      gain = arr_delay - dep_delay,
      hours = air_time / 60,
      gain_per_hour = gain / hours
      )
transmute(flights_sml,		# 只保留新添加的变量
      gain = arr_delay - dep_delay,
      hours = air_time / 60,
      gain_per_hour = gain / hours
      )

# 常用创建函数
# 模运算符
transmute(flights,
         dep_time,
         hour = dep_time %/% 100,		# %/%: 整数除法
         minute = dep_time %% 100		# %%: 求余
         )

# 偏移函数
(x <- 1:10)
lag(x)
lead(x)

# 累加和滚动聚合
x
cumsum(x)		# 累加和
cumprod(x)	# 累加积
cummin(x)		# 累加最小值
cummax(x)		# 累加最大值
cummean(x)	# 累加均值

# 排秩
y <- c(1, 2, 2, NA, 3, 4)
min_rank(y)		# 最小值获得最前面的名次
min_rank(desc(y))		# 最大值获得最前面的名次
row_number(y)
dense_rank(y)
percent_rank(y)
cume_dist(y)
```

#### 3.6 使用summarize()进行分组摘要

```R
# 3.6 使用summarize()进行分组摘要
summarize(flights, delay = mean(dep_delay, na.rm = TRUE))

# group_by()函数可以将分析单位从整个数据集更改为单个分组
# 按日期分组的一个数据框，得到每日平均延误时间
by_day <- group_by(flights, year, month, day)
summarize(by_day, delay = mean(dep_delay, na.rm = TRUE))

# 
by_test <- group_by(flights, dest)
delay <- summarize(by_test,
                  count = n(),
                  dist = mean(distance, na.rm = TRUE),
                  delay = mean(arr_delay, na.rm = TRUE)		# na.rm = TRUE在计算前去除缺失值
                  )
delay <- filter(delay, count > 20, dest != "HNL")
# 750英里内，平均延误时间会随着距离的增加而增加，接着回随着距离的增加而减小。随着飞行距离的增加，延误时间有可能会在飞行中弥补回来吗？
ggplot(data = delay, mapping = aes(x = dist, y = delay)) +
	geom_point(aes(size = count), alpha = 1/3) +
	geom_smooth(se = FALSE)
# 使用管道进行优化
delays <- flights %>%
	group_by(dest) %>%
	summarize(
  	count = n(),
  	dist = mean(distance, na.rm = TRUE),
    delay = mean(arr_delay, na.rm = TRUE)
  ) %>%
	filter(count > 20, dest != "HNL")

# 缺失值
flights %>%
	group_by(year, month, day) %>%
	summarize(mean = mean(dep_delay))

not_cancelled <- flights %>%
	filter(!is.na(dep_delay), !is.na(arr_delay))
not_cancelled %>%
	group_by(year, month, day) %>%
	summarize(mean = mean(dep_delay))

# 计数
delays <- not_cancelled %>%
	group_by(tailnum) %>%
	summarize(
  	delay = mean(arr_delay)
  )
ggplot(data = delays, mapping = aes(x = delay)) +
	geom_freqpoly(binwidth = 10)

delays <- not_cancelled %>%
	group_by(tailnum) %>%
	summarize(
  	delay = mean(arr_delay, na.rm = TRUE),
  	n = n()
  )
ggplot(data = delays, mapping = aes(x = n, y = delay)) +
	geom_point(alpha = 1 / 10)

delays %>%
	filter(n > 25) %>%
	ggplot(mapping = aes(x = n, y = delay)) +
		geom_point(alpha = 1 / 10)


# 转换成tibble, 以便输出更美观
batting <- as_tibble(Lahman::Batting)
batters <- batting %>%
	group_by(playerID) %>%
	summarize(
  ba = sum(H, na.rm = TRUE) / sum(AB, na.rm = TRUE),
  ab = sum(AB, na.rm = TRUE)
  )
batters %>%
	filter(ab > 100) %>%
	ggplot(mapping = aes(x = ab, y = ba)) +
		geom_point() +
		geom_smooth(se = FALSE)

batters %>%
	arrange(desc(ba))


# 常用的摘要函数
# 位置度量
not_cancelled %>%
	group_by(year, month, day) %>%
	summarize(
  	# 平均延误时间：
	  ave_delay1 = mean(arr_delay),
  	# 平均正延误时间：
  	ave_delay2 = mean(arr_delay[arr_delay > 0])
  )

# 分散程度度量：均方误差sd(x), 四分位距IQR(x)和绝对中位数mad(x)
# 为什么到某些目的地的距离比到其他目的地更多变
not_cancelled %>%
	group_by(dest) %>%
	summarize(distance_sd = sd(distance)) %>%
	arrange(desc(distance_sd))

# 秩的度量：min(x), quantile(x, 0.25)和max(X)
# 每天最早和最晚的航班何时出发
not_cancelled %>%
	group_by(year, month, day) %>%
	summarize(
  first = min(dep_time),
  last = max(dep_time)
  )

# 定位度量：first(x), th(x, 2)和last(x)
not_cancelled %>%
	group_by(year, month, day) %>%
	summarize(
  first_dep = first(dep_time),
  last_dep = last(dep_time)
  )
# 排秩
not_cancelled %>%
	group_by(year, month, day) %>%
	mutate(r = min_rank(desc(dep_time))) %>%
	filter(r %in% range(r))

# 计数
sum(!is.na(x))		# 计算非缺失值的数量
# 那个目的地具有最多的航空公司
not_cancelled %>%
	group_by(dest) %>%
	summarize(carriers = n_distinct(carrier)) %>%
	arrange(desc(carriers))

not_cancelled %>%
	count(dest)

# 计算每架飞机飞行的总里程
not_cancelled %>%
	count(tailnum, wt = distance)

# 逻辑值的计数和比例：sum(x > 10)和mean(y == 0)
# 多少架航班是在早上5点前出发的
not_cancelled %>%
	group_by(year, month, day) %>%
	summarize(n_early = sum(dep_time < 500))

# 延误超过1个小时的航班比例是多少
not_cancelled %>%
	group_by(year, month, day) %>%
	summarize(hour_perc = mean(arr_delay > 60))


# 按多个变量分组

```

<table>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211629419.png" alt="Fig.3.6.1" style="zoom:50%;" />
      <center>Fig.3.6.1</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211818319.png" alt="Fig.3.6.2" style="zoom:50%;" />
      <center>Fig.3.6.2</center></td>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211821530.png" alt="Fig.3.6.3" style="zoom:50%;" />
      <center>Fig.3.6.3</center></td>
  </tr>
  <tr>
    <td><img src="http://www.shminger.cn:3380/images/2024/04/21/202404211824310.png" alt="Fig.3.6.4" style="zoom:50%;" />
      <center>Fig.3.6.4</center></td>
  </tr>
</table>
