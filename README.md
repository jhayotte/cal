我是光年实验室高级招聘经理。
我在github上访问了你的开源项目，你的代码超赞。你最近有没有在看工作机会，我们在招软件开发工程师，拉钩和BOSS等招聘网站也发布了相关岗位，有公司和职位的详细信息。
我们公司在杭州，业务主要做流量增长，是很多大型互联网公司的流量顾问。公司弹性工作制，福利齐全，发展潜力大，良好的办公环境和学习氛围。
公司官网是http://www.gnlab.com,公司地址是杭州市西湖区古墩路紫金广场B座，若你感兴趣，欢迎与我联系，
电话是0571-88839161，手机号：18668131388，微信号：echo 'bGhsaGxoMTEyNAo='|base64 -D ,静待佳音。如有打扰，还请见谅，祝生活愉快工作顺利。

# cal: Go (golang) calendar library for dealing with holidays and work days

This library augments the Go time package to provide easy handling of holidays
and work days (business days).

Holiday instances can be exact days, floating days such as the 3rd Monday of
the month, yearly offsets such as the 100th day of the year, or the result of
custom function executions for complex rules.

The Calendar type provides functions for calculating workdays and dealing
with holidays that are observed on alternate days when they fall on weekends.

Here is a simple usage example of a cron job that runs once per day:
```go
package main

import (
	"time"

	"github.com/rickar/cal"
)

func main() {
	c := cal.NewCalendar()

	// add holidays for the business
	c.AddHoliday(
		cal.USIndependence,
		cal.USThanksgiving,
		cal.USChristmas,
	)

	// optionally change the default of a Mon - Fri work week
	c.SetWorkday(time.Saturday, true)

	// optionally change the holiday calculation behavior
	// (the default is US-style where weekend holidays are
	// observed on the closest weekday)
	c.Observed = cal.ObservedExact

	t := time.Now()

	// run different batch processing jobs based on the day

	if c.IsWorkday(t) {
		// create daily activity reports
	}

	if cal.IsWeekend(t) {
		// validate employee time submissions
	}

	if c.WorkdaysRemain(t) == 10 {
		// 10 business days before the end of month
		// send account statements to customers
	}

	if c.WorkdaysRemain(t) == 0 {
		// last business day of the month
		// execute auto billing transfers
	}
}
```
