## 算法学习笔记 C++日期时间类
---

主要实现日期时间的表示、操作等。

头文件：
```
#ifndef DATETIME_H_INCLUDED
#define DATETIME_H_INCLUDED

#include <iostream>
using namespace std;

class DateTime
{
private:
	int year, month, day, hour, minute,second,week;
public:
	DateTime();
	DateTime(int year, int month, int day);
	DateTime(const DateTime &d) :year(d.year), month(d.month), day(d.day),hour(d.hour),minute(d.minute),second(d.second),week(d.week){}
	DateTime(int year, int month, int day,int h,int m,int s);
	~DateTime(){}

	//得到年日月时分秒星期
	int getYear()const{ return year; }
	int getMonth()const{ return month; }
	int getDay()const{ return day; }
	int getHour()const{ return hour; }
	int getMinute()const { return minute; }
	int getSecond()const { return second; }
	int getWeek()const{ return week; }

	void setDate(int year, int month, int day);   //设置日期
	void setDateTime(int y, int m, int d, int h, int min, int s);//设置日期时间
	void setTime(int h, int m, int s);//设置时间

	static int calWeek(int y,int m,int d);//根据日期计算星期1-7
	static bool isLeapYear(int year);   //判断是否为闰年
	static int daysOfMonth(int year, int month);   //得到某个月的天数

	void show()const;   //显示日期
	DateTime changeDays(const int days)const;   //改变日期
	DateTime changeTimes(long long secs)const;   //改变时间
	int distance(const DateTime &d)const;   ////计算传入日期距离当前日期的天数
	long long secDistance(const DateTime &d)const;	////计算传入日期距离当前日期的秒数

	/*重载运算符*/

	//日期加上days个天数
	friend DateTime operator +(const DateTime &d, const int days);
	friend DateTime operator +(const int days, const DateTime &d);
	//日期加上secs个秒数
	friend DateTime operator +(const DateTime &d, const long long secs);
	friend DateTime operator +(const long long secs, const DateTime &d);
	//自身加上days个天数
	DateTime& operator +=(int days);
	//自身加上secs个秒数
	DateTime& operator +=(long long secs);

	//日期自增一天
	DateTime& operator ++();
	DateTime operator ++(int);

	//日期减去days个天数
	friend DateTime operator -(const DateTime &d, const int days);
	//日期减去secs个秒数
	friend DateTime operator -(const DateTime &d, const long long secs);

	//两个日期相减，等到差的天数
	friend int operator -(const DateTime &d1, const DateTime &d2);
	
	//自身减去days个天数
	DateTime& operator -=(int days);
	//自身减去secs个秒数
	DateTime& operator -=(long long secs);

	//日期自减一天
	DateTime& operator --();
	DateTime operator --(int);

	//日期大小比较，比较到秒
	friend bool operator >(const DateTime &d1, const DateTime &d2);
	friend bool operator >=(const DateTime &d1, const DateTime &d2);
	friend bool operator <(const DateTime &d1, const DateTime &d2);
	friend bool operator <=(const DateTime &d1, const DateTime &d2);
	friend bool operator ==(const DateTime &d1, const DateTime &d2);
	friend bool operator !=(const DateTime &d1, const DateTime &d2);

	//输出，输入日期
	friend ostream& operator <<(ostream &out, const DateTime &d);
	friend istream& operator >>(istream &in, DateTime &d);
};

#endif // DATETIME_H_INCLUDED
```

源文件cpp：
```
#ifndef DATETIME_CPP
#define DATETIME_CPP

#include "DateTime.h"
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <string>
using namespace std;

string weekStr[8] = {
	"我就是摆设",
	"星期一",
	"星期二",
	"星期三",
	"星期四",
	"星期五",
	"星期六",
	"星期日"
};

DateTime::DateTime(){
	time_t now = time(NULL);
	struct tm *ttime = localtime(&now);
	this->year = ttime->tm_year+1900;
	this->month = ttime->tm_mon+1;
	this->day = ttime->tm_mday;
	this->hour = ttime->tm_hour;
	this->minute = ttime->tm_min;
	this->second = ttime->tm_sec;
	this->week = ttime->tm_wday == 0 ? 7 : ttime->tm_wday;
}

DateTime::DateTime(int year, int month, int day) :year(year), month(month), day(day)
{
	this->hour = 0;
	this->minute = 0;
	this->second = 0;
	this->week = 1;

	if (year <= 0 || month <= 0 || month>12 || day <= 0 || day>daysOfMonth(year, month)){
		cout << "Error invalid date: ";
		show();
		cout << endl;
		exit(-1);
	}
	else{
		
		this->week = calWeek(year,month,day);
	}
}

DateTime::DateTime(int year, int month, int day,int h,int m,int s)
{
	this->year = year;
	this->month = month;
	this->day = day;
	this->hour = h;
	this->minute = m;
	this->second = s;
	this->week = 1;

	if (year <= 0 || month <= 0 || month>12 || day <= 0 || day>daysOfMonth(year, month) || h<0 || m<0 || s<0 || h>23 || m>59 || s>59){
		cout << "Error invalid";
		exit(-1);
	}
	else{
		this->week = calWeek(year, month, day);
	}
}

//设置日期
void DateTime::setDate(int year, int month, int day)
{
	this->year = year;
	this->month = month;
	this->day = day;
	this->week = calWeek(year, month, day);
}

//设置日期时间
void DateTime::setDateTime(int y, int m, int d, int h, int min, int s)
{
	this->year = y;
	this->month = m;
	this->day = d;
	this->week = calWeek(y, m, d);
	this->hour = h;
	this->minute = min;
	this->second = s;
}

// 设置时间
void DateTime::setTime(int h, int m, int s)
{
	this->hour = h;
	this->minute = m;
	this->second = s;
}

//根据日期计算星期1-7
int DateTime::calWeek(int y, int m, int d)
{
	int w;
	//保证一定是1582年10月4日之后
	if (m == 1 || m == 2) m += 12, y = y - 1;
	//蔡勒公式
	w = (d + 2 * m + 3 * (m + 1) / 5 + y + y / 4 - y / 100 + y / 400 + 1) % 7;
	
	return w == 0 ? 7 : w;

}

//判断是否为闰年
bool DateTime::isLeapYear(int year)
{
	return year % 4 == 0 && year % 100 != 0 || year % 400 == 0;
}

//得到某个月的天数
int DateTime::daysOfMonth(int year, int month)
{
	int days = 0;

	switch (month)
	{
	case 1:
	case 3:
	case 5:
	case 7:
	case 8:
	case 10:
	case 12:
		days = 31;
		break;
	case 4:
	case 6:
	case 9:
	case 11:
		days = 30;
		break;
	case 2:
		days = 28 + isLeapYear(year);
		break;
	}

	return days;
}

//显示日期
void DateTime::show()const
{
	cout << year << "-" << month << "-" << day << " " << hour << ":" << minute << ":" << second << " " << weekStr[week] << endl;
}

//改变日期
DateTime DateTime::changeDays(const int days)const
{
	int yearTemp = year;
	int monthTemp = month;
	int dayTemp = day;

	if (days>0){
		dayTemp += days;

		while (dayTemp>daysOfMonth(yearTemp, monthTemp)){
			dayTemp -= daysOfMonth(yearTemp, monthTemp);

			monthTemp++;
			if (monthTemp>12){
				yearTemp++;
				monthTemp = 1;
			}
		}
	}
	else{   //days为负数
		dayTemp += days;

		while (dayTemp<1){
			monthTemp--;
			if (monthTemp<1){
				yearTemp--;
				monthTemp = 12;
			}
			dayTemp += daysOfMonth(yearTemp, monthTemp);
		}
	}

	return DateTime(yearTemp, monthTemp, dayTemp,this->hour,this->minute,this->second);
}

//改变时间
DateTime DateTime::changeTimes(long long secs)const
{
	int htemp = hour;
	int mtemp = minute;
	int stemp = second;
	
	int f = secs >= 0LL ? 1 : -1;
	secs = f == 1 ? secs : -secs;

	int days = f*(int)(secs / 86400LL);
	secs %= 86400LL;

	stemp += f*(int)secs;
	while (stemp < 0){
		mtemp--;
		if (mtemp < 0){
			htemp--;
			if (htemp < 0){
				days--;
				htemp = 23;
			}
			mtemp = 59;
		}
		stemp += 60;
	}

	while (stemp>59){
		mtemp++;
		if (mtemp > 59){
			htemp++;
			if (htemp > 23){
				days++;
				htemp = 0;
			}
			mtemp = 0;
		}
		stemp -= 60;
	}

	DateTime d = this->changeDays(days);
	
	return DateTime(d.year,d.month,d.day,htemp,mtemp,stemp);

}

//计算传入日期距离当前日期的天数
int DateTime::distance(const DateTime &d)const
{
	//存储平年中某个月1月之前有多少天
	const int DAYS_OF_MONTH[] =
	{ 0, 31, 59, 90, 120, 151, 181, 212, 243, 273, 304, 334, 365 };

	int years = year - d.year;
	int months = DAYS_OF_MONTH[month] - DAYS_OF_MONTH[d.month];
	int days = day - d.day;

	//4年一闰，100的倍数免润，400的倍数再闰
	int totalDays = years * 365 + years / 4 - years / 100 + years / 400
		+ months + days;

	return totalDays;
}

//计算传入日期距离当前日期的秒数
long long DateTime::secDistance(const DateTime &d)const{
	int days = this->distance(d);
	long long secs = ((long long)days)*86400LL;
	secs -= ((long long)this->hour) * 3600LL + ((long long)this->minute) * 60LL + ((long long)this->second);
	secs += ((long long)d.hour) * 3600LL + ((long long)d.minute) * 60LL + ((long long)d.second);
	return secs;
}


/*重载运算符*/

//日期加上days个天数
DateTime operator +(const DateTime &d, const int days)
{
	if (days == 0){   //如果天数为0，返回当个月
		return d;
	}
	else
		return d.changeDays(days);
}

//日期加上days个天数的重载
DateTime operator +(const int days, const DateTime &d)
{
	if (days == 0){   //如果天数为0，返回当个月
		return d;
	}
	else
		return d.changeDays(days);
}


//日期加上secs个秒数
DateTime operator +(const DateTime &d, const long long secs)
{
	if (secs == 0){   //如果秒数为0不变
		return d;
	}
	else
		return d.changeTimes(secs);
}

//日期加上secs个秒数的重载
DateTime operator +(const long long secs, const DateTime &d)
{
	if (secs == 0){   //如果秒数为0不变
		return d;
	}
	else
		return d.changeTimes(secs);
}


//日期自身加上days个天数
DateTime& DateTime::operator +=(int days)
{
	if (days == 0)
		return *this;
	else{
		*this = this->changeDays(days);
		return *this;
	}
}

//日期自身加上secs个秒数
DateTime& DateTime::operator +=(long long secs)
{
	if (secs == 0)
		return *this;
	else{
		*this = this->changeTimes(secs);
		return *this;
	}
}


//日期自增一天
DateTime& DateTime::operator ++()   //前置++
{
	*this = this->changeDays(1);
	return *this;
}

DateTime DateTime::operator ++(int)   //后置++
{
	DateTime dTemp(*this);
	++(*this);
	return dTemp;
}

//日期减去days个天数
DateTime operator -(const DateTime &d, const int days)
{
	if (days == 0){   //如果天数为0，返回当个月
		return d;
	}
	else
		return d.changeDays(-days);
}

//日期减去secs个秒数
DateTime operator -(const DateTime &d, const long long secs)
{
	if (secs == 0){  
		return d;
	}
	else
		return d.changeTimes(-secs);
}

//两个日期相减
int operator -(const DateTime &d1, const DateTime &d2)
{
	return d1.distance(d2);
}


//日期自身减去days个天数
DateTime& DateTime::operator -=(int days)
{
	if (days == 0)
		return *this;
	else{
		*this = this->changeDays(-days);
		return *this;
	}
}

//日期自身减去secs个秒数
DateTime& DateTime::operator -=(long long secs)
{
	if (secs == 0)
		return *this;
	else{
		*this = this->changeTimes(-secs);
		return *this;
	}
}

//日期自减一天
DateTime& DateTime::operator--()   //前置--
{
	*this = this->changeDays(-1);
	return *this;
}

DateTime DateTime::operator--(int)   //后置--
{
	DateTime dTemp(*this);
	--(*this);
	return dTemp;
}

//重载大小比较运算符
bool operator >(const DateTime &d1, const DateTime &d2)
{
	return d1.secDistance(d2)>0LL ? true : false;
}

bool operator >=(const DateTime &d1, const DateTime &d2)
{
	return d1.secDistance(d2) >= 0LL ? true : false;
}

bool operator <(const DateTime &d1, const DateTime &d2)
{
	return d1.secDistance(d2)<0LL ? true : false;
}

bool operator <=(const DateTime &d1, const DateTime &d2)
{
	return d1.secDistance(d2) <= 0LL ? true : false;
}

bool operator ==(const DateTime &d1, const DateTime &d2)
{
	return d1.secDistance(d2) == 0LL ? true : false;
}

bool operator !=(const DateTime &d1, const DateTime &d2)
{
	return d1.secDistance(d2) != 0LL ? true : false;
}

//重载输入输出运算符
ostream& operator <<(ostream &out, const DateTime &d)
{
	out << d.getYear() << "-"
		<< d.getMonth() << "-"
		<< d.getDay() << " "
		<< d.getHour() << ":"
		<< d.getMinute() << ":"
		<< d.getSecond() << " "
		<< weekStr[d.getWeek()]
		<<endl;

	return out;
}

istream& operator >>(istream &in, DateTime &d)
{
	int year, month, day,h,m,s;

	cout << "Input year month day hour minute second:" << endl;
	in >> year >> month >> day >> h >> m >> s;

	d.setDateTime(year, month, day,h,m,s);

	return in;
}

#endif // DATETIME_CPP
```

---

#### [返回目录](./)