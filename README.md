# EastAsiaCalendars README

EastAsiaCalendars provides an ```eacal``` Python module for accessing
East Asia calendar systems, originated in China, and spread to Korea,
Vietnam, and Japan. This module includes the following.

- [solar terms](http://en.wikipedia.org/wiki/Solar_term) (節氣, 节气, 節気, 절기, tiết khí)
- [sexagenary cycle](http://en.wikipedia.org/wiki/Sexagenary_cycle) (六十花甲, 干支, 간지, Gānzhī)
- [zassetsu](http://ja.wikipedia.org/wiki/%E9%9B%91%E7%AF%80) (Seasonal days in the Japanese calendar)

## Requirements

- Python 2.7
- [PyEphem](http://rhodesmill.org/pyephem/)
- [pytz](http://pytz.sourceforge.net/)
- [jdcal](https://pypi.python.org/pypi/jdcal)

## Installation

```bash
pip install pyephem
pip install pytz
pip install jdcal
python setup.py install
```

## Example & Usage

### Calculating solar terms in a year

The solar terms of 2015 for English (in UTC).

```py
>>> import eacal
>>> from datetime import datetime
>>> c = eacal.EACal()
>>> for x in c.get_annual_solar_terms(2015):
...     print "%-25s %s" % (x[0], datetime.strftime(x[2], "%Y-%m-%d %H:%M %Z"))
... 
minor cold                2015-01-05 16:20 UTC
major cold                2015-01-20 09:43 UTC
start of spring           2015-02-04 03:58 UTC
rain water                2015-02-18 23:49 UTC
awakening of insects      2015-03-05 21:55 UTC
vernal equinox            2015-03-20 22:45 UTC
...
major snow                2015-12-07 10:53 UTC
winter solstice           2015-12-22 04:47 UTC
```

The solar terms of 2015, for Traditional Chinese (in Hong Kong Time), Simplified Chinese (in Chinese Standard Time), Japanese (in Japan Standard Time), Korean (in Korea Standard Time), and Vietnamese (in Indochina Time).

```py
>>> import eacal
>>> from datetime import datetime
>>> c_t = eacal.EACal(zh_t=True)
>>> for x in c_t.get_annual_solar_terms(2015):
...     print "%s %s" % (x[0], datetime.strftime(x[2], "%Y-%m-%d %H:%M %Z"))
小寒 2015-01-06 00:20 HKT
大寒 2015-01-20 17:43 HKT
立春 2015-02-04 11:58 HKT
雨水 2015-02-19 07:49 HKT
驚蟄 2015-03-06 05:55 HKT
春分 2015-03-21 06:45 HKT
...
大雪 2015-12-07 18:53 HKT
冬至 2015-12-22 12:47 HKT

>>> c_s = eacal.EACal(zh_s=True)
>>> for x in c_s.get_annual_solar_terms(2015):
...     print "%s %s" % (x[0], datetime.strftime(x[2], "%Y-%m-%d %H:%M %Z"))
小寒 2015-01-06 00:20 CST
大寒 2015-01-20 17:43 CST
立春 2015-02-04 11:58 CST
雨水 2015-02-19 07:49 CST
惊蛰 2015-03-06 05:55 CST
春分 2015-03-21 06:45 CST
...
大雪 2015-12-07 18:53 CST
冬至 2015-12-22 12:47 CST

>>> c_j = eacal.EACal(ja=True)
>>> for x in c_j.get_annual_solar_terms(2015):
...     print "%s %s" % (x[0], datetime.strftime(x[2], "%Y-%m-%d %H:%M %Z"))
小寒 2015-01-06 01:20 JST
大寒 2015-01-20 18:43 JST
立春 2015-02-04 12:58 JST
雨水 2015-02-19 08:49 JST
啓蟄 2015-03-06 06:55 JST
春分 2015-03-21 07:45 JST
...
大雪 2015-12-07 19:53 JST
冬至 2015-12-22 13:47 JST

>>> c_k = eacal.EACal(ko=True)
>>> for x in c_k.get_annual_solar_terms(2015):
...     print "%s %s" % (x[0], datetime.strftime(x[2], "%Y-%m-%d %H:%M %Z"))
소한 2015-01-06 01:20 KST
대한 2015-01-20 18:43 KST
입춘 2015-02-04 12:58 KST
우수 2015-02-19 08:49 KST
경칩 2015-03-06 06:55 KST
춘분 2015-03-21 07:45 KST
...
대설 2015-12-07 19:53 KST
동지 2015-12-22 13:47 KST

>>> c_v = eacal.EACal(vi=True)
>>> for x in c_v.get_annual_solar_terms(2015):
...     print "%-12s %s" % (x[0], datetime.strftime(x[2], "%Y-%m-%d %H:%M %Z"))
Tiểu hàn     2015-01-05 23:20 ICT
Đại hàn      2015-01-20 16:43 ICT
Lập xuân     2015-02-04 10:58 ICT
Vũ thủy      2015-02-19 06:49 ICT
Kinh trập    2015-03-06 04:55 ICT
Xuân phân    2015-03-21 05:45 ICT
...
Đại tuyết    2015-12-07 17:53 ICT
Đông chí     2015-12-22 11:47 ICT
```

The solar terms of 2015 in North American Eastern Time Zone.

```py
>>> import eacal
>>> import pytz
>>> from datetime import datetime
>>> c = eacal.EACal(tz=pytz.timezone('America/New_York'))
>>> for x in c.get_annual_solar_terms(2015):
...     print "%-25s %s" % (x[0], datetime.strftime(x[2], "%Y-%m-%d %H:%M %Z"))
minor cold                2015-01-05 11:20 EST
major cold                2015-01-20 04:43 EST
start of spring           2015-02-03 22:58 EST
rain water                2015-02-18 18:49 EST
awakening of insects      2015-03-05 16:55 EST
vernal equinox            2015-03-20 18:45 EDT  # in DST
...
major snow                2015-12-07 05:53 EST
winter solstice           2015-12-21 23:47 EST
```


### Calculating sexagenary cycles

Calculating the cyclic year of 2015.

```py
>>> import eacal
>>> print(eacal.EACal().get_cycle_year(2015))
wood-yin goat   # 乙未
>>> print(eacal.EACal(zh_t=True).get_cycle_year(2015))
乙未
>>> print(eacal.EACal(vi=True).get_cycle_year(2015))
ất mùi   # 乙未
```

Calculating the Cyclic month of May 2015.

```py
>>> import eacal
>>> print(eacal.EACal().get_cycle_month(2015, 5))
metal-yin snake   # 辛巳
>>> print(eacal.EACal(ja=True).get_cycle_month(2015, 5))
辛巳
>>> print(eacal.EACal(ko=True).get_cycle_month(2015, 5))
신사   # 辛巳
```

Calculating the Cyclic day of 10th, May 2015.
```py
>>> import eacal
>>> from datetime import date
>>> print(eacal.EACal().get_cycle_day(date(2015, 5, 10)))
fire-yang dog   # 丙戌
>>> print(eacal.EACal(zh_s=True).get_cycle_day(date(2015, 5, 10)))
丙戌
>>> print(eacal.EACal(vi=True).get_cycle_day(date(2015, 5, 10)))
bính tuất   # 丙戌
```

Calculating the Cyclic year, month, and day around the start of spring in 2015.
```py
>>> import eacal
>>> from datetime import datetime
>>> c = eacal.EACal()     # for English, in UTC
>>> print('|'.join(c.get_cycle_ymd(datetime(2015, 2, 3))))
wood-yang horse|fire-yin ox|metal-yang dog     # 甲午年 丁丑月 庚戌日
>>> print('|'.join(c.get_cycle_ymd(datetime(2015, 2, 4))))
wood-yin goat|earth-yang tiger|metal-yin pig   # 乙未年 戊寅月 辛亥日 (cyclic year and cyclic month incremented at the start of spring)
>>> print('|'.join(c.get_cycle_ymd(datetime(2015, 2, 5))))
wood-yin goat|earth-yang tiger|water-yang rax  # 乙未年 戊寅月 壬子日
>>> print(c.get_cycle_ymd(datetime(2015, 2, 3), id=True))
(30, 13, 46)    # 30=wood-yang horse, 13=fire-yin ox, 46=metal-yang dog
>>> print(c.get_cycle_ymd(datetime(2015, 2, 4), id=True))
(31, 14, 47)    # 31=wood-yin goat, 14=earth-yang tiger, 47=metal-yin pig
>>> print(c.get_cycle_ymd(datetime(2015, 2, 5), id=True))
(31, 14, 48)    # 48=water-yang rax
```


## TODO

- a method for finding days which have a specified sexagenary cycle.
- regnal years
