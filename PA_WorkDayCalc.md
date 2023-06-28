power Automate 工作日計算
輸入兩組日期
計算中日期間的工作天

宣告所需變數
![Alt text](image.png)
<br/>

Date Different Expression
```
dateDifference(variables('DateNow'),variables('InplementDate'))
```
日期相減後結果為一組字串
```
"相差日數.時:分:秒"
```

把得到的值存到變數里
![Alt text](image-1.png)
Expression
```
if(
    less(
        int(split(variables('DateDiffStr'),'.')[0]),0),
        0,
        int(split(variables('DateDiffStr'),'.')[0])
)
```
根據相差日數建表
![Alt text](image-2.png)
Expression
<br/>
```
range: range(0,variables('DateDiff'))
Date: formatDateTime(addDays(variables('DateNow'),item()),'yyyy-MM-dd')
WeekDay: dayOfWeek(addDays(variables('DateNow'),item()))
```
``Select`` 回傳一個 `Array`
根據WeekDay的值 ``Filter`` 結果

把 ```WeekDay = 6``` 跟 ```WeekDay = 0 ``` 篩掉
![Alt text](image-3.png)

最後得到的陣列長度就是兩個日期的工作天
Expression
```
length(body('Filter_Week_Day_2'))
```