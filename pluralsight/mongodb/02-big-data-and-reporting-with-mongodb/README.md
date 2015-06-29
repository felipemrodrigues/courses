# [Big Data & Reporting with MongoDB][0]

[Data][1]

Data structure:

```
> db.zips.findOne()
{
  "_id" : "01007",
  "city" : "BELCHERTOWN",
  "loc" : [
    -72.410953,
    42.275103
  ],
  "pop" : 10579,
  "state" : "MA"
}
```

## 3. The $group Pipeline Operator

### Simple $group

```
> var s1 = { "$group" : { "_id" : "all", "sum" : { "$sum" : 1 } } }
> db.zips.aggregate(s1)
{ "_id" : "all", "sum" : 29353 }
```

### $min $max $avg

```
> var s1 = { $group : { _id : "all", avg : { $avg : "$pop" } } }
> db.zips.aggregate(s1)
{ "_id" : "all", "avg" : 8462.794262937348 }
```

```
> var s1 = { $group : { _id : "all", min : { $min : "$pop" } } }
> db.zips.aggregate(s1)
{ "_id" : "all", "min" : 0 }
```

```
> var s1 = { $group : { _id : "all", max : { $max : "$pop" } } }
> db.zips.aggregate(s1)
{ "_id" : "all", "max" : 112047 }
```

```
> var s1 = { $group : { _id : "all", sum : { $sum : 1 }, avg : { $avg : "$pop" }, min : { $min : "$pop" }, max : { $max : "$pop" }}}
> db.zips.aggregate(s1)
{ "_id" : "all", "sum" : 29353, "avg" : 8462.794262937348, "min" : 0, "max" : 112047 }
```

### Group by field

```
> var s1 = { $group : { _id : "$state", sum : { $sum : 1 }}}
> db.zips.aggregate(s1)
{ "_id" : "WA", "sum" : 484 }
{ "_id" : "HI", "sum" : 80 }
{ "_id" : "CA", "sum" : 1516 }
{ "_id" : "OR", "sum" : 384 }
{ "_id" : "NM", "sum" : 276 }
{ "_id" : "UT", "sum" : 205 }
{ "_id" : "OK", "sum" : 586 }
{ "_id" : "LA", "sum" : 464 }
{ "_id" : "NE", "sum" : 574 }
{ "_id" : "TX", "sum" : 1671 }
{ "_id" : "MO", "sum" : 994 }
{ "_id" : "MT", "sum" : 314 }
{ "_id" : "ND", "sum" : 391 }
{ "_id" : "AK", "sum" : 195 }
{ "_id" : "SD", "sum" : 384 }
{ "_id" : "DC", "sum" : 24 }
{ "_id" : "MN", "sum" : 882 }
{ "_id" : "ID", "sum" : 244 }
{ "_id" : "KY", "sum" : 809 }
{ "_id" : "WI", "sum" : 716 }
{ "_id" : "TN", "sum" : 582 }
{ "_id" : "AZ", "sum" : 270 }
{ "_id" : "CO", "sum" : 414 }
{ "_id" : "KS", "sum" : 715 }
{ "_id" : "MS", "sum" : 363 }
{ "_id" : "FL", "sum" : 804 }
{ "_id" : "IA", "sum" : 922 }
{ "_id" : "NC", "sum" : 705 }
{ "_id" : "VA", "sum" : 816 }
{ "_id" : "IN", "sum" : 676 }
{ "_id" : "ME", "sum" : 410 }
{ "_id" : "WV", "sum" : 656 }
{ "_id" : "MD", "sum" : 420 }
{ "_id" : "GA", "sum" : 635 }
{ "_id" : "NH", "sum" : 218 }
{ "_id" : "NV", "sum" : 104 }
{ "_id" : "DE", "sum" : 53 }
{ "_id" : "AL", "sum" : 567 }
{ "_id" : "CT", "sum" : 263 }
{ "_id" : "SC", "sum" : 350 }
{ "_id" : "RI", "sum" : 69 }
{ "_id" : "PA", "sum" : 1458 }
{ "_id" : "VT", "sum" : 243 }
{ "_id" : "MA", "sum" : 474 }
{ "_id" : "WY", "sum" : 140 }
{ "_id" : "MI", "sum" : 876 }
{ "_id" : "OH", "sum" : 1007 }
{ "_id" : "AR", "sum" : 578 }
{ "_id" : "IL", "sum" : 1237 }
{ "_id" : "NJ", "sum" : 540 }
{ "_id" : "NY", "sum" : 1595 }
```

```
> var s1 = { $group : { _id : "$state", sum : { $sum : 1 }, avg : { $avg : "$pop" }, min : { $min : "$pop" }, max : { $max : "$pop" }}}
> db.zips.aggregate(s1)
{ "_id" : "WA", "sum" : 484, "avg" : 10055.148760330578, "min" : 2, "max" : 50515 }
{ "_id" : "HI", "sum" : 80, "avg" : 13852.8625, "min" : 0, "max" : 62915 }
{ "_id" : "CA", "sum" : 1516, "avg" : 19627.236147757256, "min" : 0, "max" : 99568 }
{ "_id" : "OR", "sum" : 384, "avg" : 7401.877604166667, "min" : 0, "max" : 48007 }
{ "_id" : "NM", "sum" : 276, "avg" : 5489.380434782609, "min" : 0, "max" : 57502 }
{ "_id" : "UT", "sum" : 205, "avg" : 8404.146341463415, "min" : 9, "max" : 55999 }
{ "_id" : "OK", "sum" : 586, "avg" : 5367.892491467577, "min" : 8, "max" : 45542 }
{ "_id" : "LA", "sum" : 464, "avg" : 9089.644396551725, "min" : 0, "max" : 58905 }
{ "_id" : "NE", "sum" : 574, "avg" : 2749.3710801393727, "min" : 5, "max" : 35325 }
{ "_id" : "TX", "sum" : 1671, "avg" : 10164.333333333334, "min" : 0, "max" : 79463 }
{ "_id" : "MO", "sum" : 994, "avg" : 5141.496981891348, "min" : 0, "max" : 54994 }
{ "_id" : "MT", "sum" : 314, "avg" : 2544.420382165605, "min" : 7, "max" : 40121 }
{ "_id" : "ND", "sum" : 391, "avg" : 1632.4092071611253, "min" : 12, "max" : 42195 }
{ "_id" : "AK", "sum" : 195, "avg" : 2793.3230769230768, "min" : 0, "max" : 32383 }
{ "_id" : "SD", "sum" : 384, "avg" : 1810.9296875, "min" : 8, "max" : 45328 }
{ "_id" : "DC", "sum" : 24, "avg" : 25287.5, "min" : 11, "max" : 62924 }
{ "_id" : "MN", "sum" : 882, "avg" : 4958.02947845805, "min" : 0, "max" : 51421 }
{ "_id" : "ID", "sum" : 244, "avg" : 4126.020491803279, "min" : 0, "max" : 40912 }
{ "_id" : "KY", "sum" : 809, "avg" : 4543.243510506799, "min" : 0, "max" : 46563 }
{ "_id" : "WI", "sum" : 716, "avg" : 6832.079608938548, "min" : 2, "max" : 57187 }
{ "_id" : "TN", "sum" : 582, "avg" : 8378.792096219931, "min" : 2, "max" : 60508 }
{ "_id" : "AZ", "sum" : 270, "avg" : 13574.918518518518, "min" : 2, "max" : 57131 }
{ "_id" : "CO", "sum" : 414, "avg" : 7955.929951690821, "min" : 0, "max" : 59418 }
{ "_id" : "KS", "sum" : 715, "avg" : 3461.937062937063, "min" : 0, "max" : 50178 }
{ "_id" : "MS", "sum" : 363, "avg" : 7088.749311294766, "min" : 0, "max" : 46968 }
{ "_id" : "FL", "sum" : 804, "avg" : 15779.407960199005, "min" : 0, "max" : 73194 }
{ "_id" : "IA", "sum" : 922, "avg" : 3011.301518438178, "min" : 12, "max" : 52105 }
{ "_id" : "NC", "sum" : 705, "avg" : 9402.321985815603, "min" : 0, "max" : 69179 }
{ "_id" : "VA", "sum" : 816, "avg" : 7575.341911764706, "min" : 0, "max" : 68525 }
{ "_id" : "IN", "sum" : 676, "avg" : 8201.384615384615, "min" : 75, "max" : 56543 }
{ "_id" : "ME", "sum" : 410, "avg" : 2991.8243902439026, "min" : 0, "max" : 40434 }
{ "_id" : "WV", "sum" : 656, "avg" : 2733.454268292683, "min" : 0, "max" : 70185 }
{ "_id" : "MD", "sum" : 420, "avg" : 11384.235714285714, "min" : 1, "max" : 76002 }
{ "_id" : "GA", "sum" : 635, "avg" : 10201.914960629922, "min" : 0, "max" : 58646 }
{ "_id" : "NH", "sum" : 218, "avg" : 5088.311926605505, "min" : 27, "max" : 41438 }
{ "_id" : "NV", "sum" : 104, "avg" : 11556.086538461539, "min" : 1, "max" : 51532 }
{ "_id" : "DE", "sum" : 53, "avg" : 12569.207547169812, "min" : 108, "max" : 50573 }
{ "_id" : "AL", "sum" : 567, "avg" : 7126.255731922399, "min" : 0, "max" : 44165 }
{ "_id" : "CT", "sum" : 263, "avg" : 12498.539923954373, "min" : 25, "max" : 60670 }
{ "_id" : "SC", "sum" : 350, "avg" : 9962.00857142857, "min" : 0, "max" : 66990 }
{ "_id" : "RI", "sum" : 69, "avg" : 14539.391304347826, "min" : 45, "max" : 53733 }
{ "_id" : "PA", "sum" : 1458, "avg" : 8149.275034293552, "min" : 0, "max" : 80454 }
{ "_id" : "VT", "sum" : 243, "avg" : 2315.8765432098767, "min" : 0, "max" : 39127 }
{ "_id" : "MA", "sum" : 474, "avg" : 12692.879746835442, "min" : 0, "max" : 65046 }
{ "_id" : "WY", "sum" : 140, "avg" : 3239.4857142857145, "min" : 6, "max" : 33107 }
{ "_id" : "MI", "sum" : 876, "avg" : 10611.069634703197, "min" : 0, "max" : 84712 }
{ "_id" : "OH", "sum" : 1007, "avg" : 10771.119165839125, "min" : 38, "max" : 66674 }
{ "_id" : "AR", "sum" : 578, "avg" : 4066.998269896194, "min" : 0, "max" : 53532 }
{ "_id" : "IL", "sum" : 1237, "avg" : 9238.137429264349, "min" : 0, "max" : 112047 }
{ "_id" : "NJ", "sum" : 540, "avg" : 14315.162962962962, "min" : 17, "max" : 69646 }
{ "_id" : "NY", "sum" : 1595, "avg" : 11279.248902821317, "min" : 0, "max" : 111396 }
```

### Value-of-field

```
> var s2 = { $group : { _id : "$sku", min : { $min : "$item.qty" }}}
```

### Field name

```
> var s1 = { $group : { _id : "all", "some field name" : { $sum : 1 }}}
> db.zips.aggregate(s1)
{ "_id" : "all", "some field name" : 29353 }
```

### $addToSet

```
> var s1 = { $group : { _id : "all", states : { $addToSet : "$state" }}}
> db.zips.aggregate(s1)
{ "_id" : "all", "states" : [ "WA", "HI", "CA", "OR", "NM", "UT", "OK", "LA", "NE", "TX", "MO", "MT", "ND", "AK", "SD", "DC", "MN", "ID", "KY", "WI", "TN", "AZ", "CO", "KS", "MS", "FL", "IA", "NC", "VA", "IN", "ME", "WV", "MD", "GA", "NH", "NV", "DE", "AL", "CT", "SC", "RI", "PA", "VT", "MA", "WY", "MI", "OH", "AR", "IL", "NJ", "NY" ] }
```

### $push

```
> var s1 = { $group : { _id : "all", states : { $push : "$state" }}}
> db.zips.aggregate(s1)
# Will push every item in the array repeatedly
```

### $first

```
> var s1 = { $group : { _id : "$state", sample : { $first : "$city" }}}
> db.zips.aggregate(s1)
{ "_id" : "WA", "sample" : "ALGONA" }
{ "_id" : "HI", "sample" : "ELEELE" }
{ "_id" : "CA", "sample" : "LOS ANGELES" }
{ "_id" : "OR", "sample" : "AURORA" }
{ "_id" : "NM", "sample" : "ALGODONES" }
{ "_id" : "UT", "sample" : "ALTAMONT" }
{ "_id" : "OK", "sample" : "ALEX" }
{ "_id" : "LA", "sample" : "METAIRIE" }
{ "_id" : "NE", "sample" : "ABIE" }
{ "_id" : "TX", "sample" : "ALLEN" }
{ "_id" : "MO", "sample" : "MANCHESTER" }
{ "_id" : "MT", "sample" : "ACTON" }
{ "_id" : "ND", "sample" : "ALICE" }
{ "_id" : "AK", "sample" : "ANCHORAGE" }
{ "_id" : "SD", "sample" : "AURORA" }
{ "_id" : "DC", "sample" : "WASHINGTON" }
{ "_id" : "MN", "sample" : "EAST BETHEL" }
{ "_id" : "ID", "sample" : "FORT HALL" }
{ "_id" : "KY", "sample" : "BARDSTOWN" }
{ "_id" : "WI", "sample" : "ADELL" }
.
.
.
```

### $last

```
> var s1 = { $group : { _id : "$state", city : { $last : "$city" }}}
> db.zips.aggregate(s1)
{ "_id" : "WA", "city" : "DAYTON" }
{ "_id" : "HI", "city" : "HONOLULU" }
{ "_id" : "CA", "city" : "CARNELIAN BAY" }
{ "_id" : "OR", "city" : "PRAIRIE CITY" }
{ "_id" : "NM", "city" : "BELL RANCH" }
{ "_id" : "UT", "city" : "PAROWAN" }
{ "_id" : "OK", "city" : "OCTAVIA" }
{ "_id" : "LA", "city" : "WINNFIELD" }
{ "_id" : "NE", "city" : "LAKESIDE" }
{ "_id" : "TX", "city" : "EL PASO" }
{ "_id" : "MO", "city" : "SPRINGFIELD" }
{ "_id" : "MT", "city" : "WHITEFISH" }
{ "_id" : "ND", "city" : "SURREY" }
{ "_id" : "AK", "city" : "ANGOON" }
{ "_id" : "SD", "city" : "ZEONA" }
{ "_id" : "DC", "city" : "WASHINGTON" }
{ "_id" : "MN", "city" : "SAINT VINCENT" }
{ "_id" : "ID", "city" : "WORLEY" }
{ "_id" : "KY", "city" : "MILLTOWN" }
{ "_id" : "WI", "city" : "WINNECONNE" }
.
.
.
```

## 4. Document Selection

### $match

```
> var s3 = { $match : { state : "CA" }}
> db.zips.aggregate(s3)
{ "_id" : "90001", "city" : "LOS ANGELES", "loc" : [ -118.247896, 33.973093 ], "pop" : 51841, "state" : "CA" }
{ "_id" : "90002", "city" : "LOS ANGELES", "loc" : [ -118.246213, 33.94969 ], "pop" : 40629, "state" : "CA" }
{ "_id" : "90003", "city" : "LOS ANGELES", "loc" : [ -118.272739, 33.965335 ], "pop" : 53938, "state" : "CA" }
{ "_id" : "90005", "city" : "LOS ANGELES", "loc" : [ -118.301197, 34.058508 ], "pop" : 35864, "state" : "CA" }
{ "_id" : "90004", "city" : "LOS ANGELES", "loc" : [ -118.302863, 34.076163 ], "pop" : 64062, "state" : "CA" }
{ "_id" : "90006", "city" : "LOS ANGELES", "loc" : [ -118.291687, 34.049323 ], "pop" : 63389, "state" : "CA" }
{ "_id" : "90007", "city" : "LOS ANGELES", "loc" : [ -118.287095, 34.029442 ], "pop" : 46985, "state" : "CA" }
{ "_id" : "90008", "city" : "LOS ANGELES", "loc" : [ -118.341123, 34.011643 ], "pop" : 33073, "state" : "CA" }
{ "_id" : "90010", "city" : "LOS ANGELES", "loc" : [ -118.302664, 34.060633 ], "pop" : 5335, "state" : "CA" }
{ "_id" : "90011", "city" : "LOS ANGELES", "loc" : [ -118.258189, 34.007856 ], "pop" : 96074, "state" : "CA" }
{ "_id" : "90012", "city" : "LOS ANGELES", "loc" : [ -118.238479, 34.061396 ], "pop" : 28518, "state" : "CA" }
{ "_id" : "90014", "city" : "LOS ANGELES", "loc" : [ -118.250937, 34.044272 ], "pop" : 2715, "state" : "CA" }
{ "_id" : "90013", "city" : "LOS ANGELES", "loc" : [ -118.243366, 34.044841 ], "pop" : 5653, "state" : "CA" }
{ "_id" : "90015", "city" : "LOS ANGELES", "loc" : [ -118.271613, 34.043439 ], "pop" : 18880, "state" : "CA" }
{ "_id" : "90017", "city" : "LOS ANGELES", "loc" : [ -118.266582, 34.055864 ], "pop" : 21790, "state" : "CA" }
{ "_id" : "90016", "city" : "LOS ANGELES", "loc" : [ -118.352787, 34.029826 ], "pop" : 43669, "state" : "CA" }
{ "_id" : "90018", "city" : "LOS ANGELES", "loc" : [ -118.315173, 34.028972 ], "pop" : 48267, "state" : "CA" }
{ "_id" : "90019", "city" : "LOS ANGELES", "loc" : [ -118.33426, 34.048158 ], "pop" : 64996, "state" : "CA" }
{ "_id" : "90020", "city" : "LOS ANGELES", "loc" : [ -118.302211, 34.066535 ], "pop" : 34926, "state" : "CA" }
{ "_id" : "90021", "city" : "LOS ANGELES", "loc" : [ -118.244698, 34.033303 ], "pop" : 2869, "state" : "CA" }
.
.
.
```

### $match and Arrays

```
> var s3 = { $match : { loc : 42.275103 }}
> db.zips.aggregate(s3)
{ "_id" : "01007", "city" : "BELCHERTOWN", "loc" : [ -72.410953, 42.275103 ], "pop" : 10579, "state" : "MA" }
```

[0]: http://www.pluralsight.com/courses/mongodb-big-data-reporting
[1]: http://media.mongodb.org/zips.json