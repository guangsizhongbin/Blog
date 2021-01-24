---
title: "SolarToLunar"
date: 2021-01-24T22:13:38+08:00
lastmod: 2021-01-24
author: "xiaonan"
math:
 enable: true

tags: [python]
categories: [python]
---


### sxtw[^用sxtwl模块轻松实现农历转换]
[^用sxtwl模块轻松实现农历转换]:[用sxtwl模块轻松实现农历转换](https://zhuanlan.zhihu.com/p/105710849)

```python
import sxtwl

def lunar_calendar(yyyy,mm,dd):
        import sxtwl
        lunar = sxtwl.Lunar()
        daylunar = lunar.getDayBySolar(yyyy, mm, dd)
        if daylunar.Lmc > 1:
            ly, lmm = str(daylunar.y), str(daylunar.Lmc - 1)
        else:
            ly, lmm = str(daylunar.y - 1), str(daylunar.Lmc + 11)
        if daylunar.Lleap:
            lm="闰"+lmm
        else:
            lm=lmm
        ld=str(daylunar.Ldi+1)

        ShX = ["鼠", "牛", "虎", "兔", "龙", "蛇", "马", "羊", "猴", "鸡", "狗", "猪"]
        sx = ShX[daylunar.Lyear2.dz]
        return ly,lm,ld,sx

lunar = lunar_calendar(2021,1,24)
print(lunar[0] + "年" + lunar[1] + "月" + lunar[2] + "日")
```

