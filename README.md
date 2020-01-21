# 日期方法

## 常用如下

```js
var date = new Date(); //中国标准时间
var year = date.getFullYear(); //获取完整的年份(4位)
var month = date.getMonth(); //获取当前月份(0-11,0代表1月)
var nowDate = date.getDate(); //获取当前日(1-31)
var day = date.getDay(); //获取当前星期X(0-6,0代表星期天)
```

## 格式化日期

1. yyyy-MM-dd

```js
//格式化日期：yyyy-MM-dd
function formatDate(date) {
  var myyear = date.getFullYear();
  var mymonth = date.getMonth() + 1;
  var myweekday = date.getDate();

  if (mymonth < 10) {
    mymonth = "0" + mymonth;
  }
  if (myweekday < 10) {
    myweekday = "0" + myweekday;
  }
  return myyear + "-" + mymonth + "-" + myweekday; //想要什么格式都可以随便自己拼
}

var date = new Date();
//date
//Tue Jan 21 2020 07:56:57 GMT+0800 (中国标准时间)
formatDate(date);
//"2020-01-21"
```

或者

```js
function formatDate(dateArg) {
  const date = new Date(dateArg);
  const year = date.getFullYear();
  const month = date.getMonth() + 1;
  const day = date.getDate();
  const formatMonth = month < 10 ? `0${month}` : month;
  const formatDay = day < 10 ? `0${day}` : day;

  return `${year}-${formatMonth}-${formatDay}`;
}
```

2. xx 年 xx 月 xx 日 xx 时 xx 分

```js
//获取当前日期 时间
function todayTime() {
  var date = new Date();
  var curYear = date.getFullYear();
  var curMonth = date.getMonth() + 1;
  var curDate = date.getDate();
  if (curMonth < 10) {
    curMonth = "0" + curMonth;
  }
  if (curDate < 10) {
    curDate = "0" + curDate;
  }
  var curHours = date.getHours();
  var curMinutes = date.getMinutes();
  var curtime =
    curYear +
    " 年 " +
    curMonth +
    " 月 " +
    curDate +
    " 日" +
    curHours +
    "时 " +
    curMinutes +
    "分 ";
  return curtime;
}
```

3. 英文格式日期

```js
//获取当前日期 英文
function todayTimeEn() {
  var dt = new Date();
  var m = new Array(
    "January",
    "February",
    "March",
    "April",
    "May",
    "June",
    "July",
    "August",
    "September",
    "October",
    "November",
    "December"
  );
  mn = dt.getMonth();
  dn = dt.getDate();
  if (dn < 10) {
    dn = "0" + dn;
  }
  var curtime = m[mn] + " " + dn + ", " + dt.getFullYear();
  return curtime;
}
```

4. 自定义任意格式

```js
Date.prototype.Format = function(fmt) {
  var o = {
    "M+": this.getMonth() + 1, // 月份
    "d+": this.getDate(), // 日
    "h+": this.getHours(), // 小时
    "m+": this.getMinutes(), // 分
    "s+": this.getSeconds(), // 秒
    "q+": Math.floor((this.getMonth() + 3) / 3), // 季度
    S: this.getMilliseconds()
    // 毫秒
  };
  if (/(y+)/.test(fmt))
    fmt = fmt.replace(
      RegExp.$1,
      (this.getFullYear() + "").substr(4 - RegExp.$1.length)
    );
  for (var k in o)
    if (new RegExp("(" + k + ")").test(fmt))
      fmt = fmt.replace(
        RegExp.$1,
        RegExp.$1.length == 1 ? o[k] : ("00" + o[k]).substr(("" + o[k]).length)
      );
  return fmt;
};
```

使用方法

```js
new Date().Format("yyyy-MM-dd hh:mm");
//console.log打印结果： "2019-08-22 16:42"

new Date().Format("yyyy.MM.dd hh:mm");
//console.log打印结果： "2019.08.22 16:44"

new Date().Format("yyyy-MM-dd");
//console.log打印结果："2019-08-22"
```
