# TP-Date
The goal of this project was to implement a simple date class and to then design tests according to the implementation.<br>
The first thing I did was using Input Space Partitioning to design the first tests:<br>

I decided to use this as an input space for isValidDate and for the constructor:

|                         | b1          | b2                          | b3                        | b4          | b5          |
| ----------------------- | ----------- | -----------                 | -----------               | ----------- | ----------- |
| q1       Value of year  | <=0         |  leap year                  | common year               |             |             |
| q2       Value of month | <=0         |  {1,3,5,7,8, 10, 12}        |  { 4, 6, 9, 11}           |  2          |  >12        |
| q3       Value of day   | <=0         | >= 1 and <=max(month,year)  |  >max(month,year)         |             |             |

For the function isLeapYear, I decided to take inputs that are either leap year or non leap year depending if the date is divisible by 4, divisible by 100 and divisible by 400.

For the compareTo method, the input space that I chose was 4 different cases, one where "this" is posterior to "other",anterior,equal and then when other is null.
Since the method compareTo has been tested we can now use it to test nextDate and previousDate.

For the method nextDate, we decided to take inputs that makes an impact on other parameters so:
|                         | b1                     | b2           | b3           |
| ----------------------- | -----------            | -----------  | ------------ |
| q1       Value of year  | leap year              | common year  |              |
| q2       Value of month | last month of the year | common month | February     |
| q3       Value of day   | last day of the month  | common day   |              |

Quite similarly to the method previousDate, we used this input for the method previousDate:
|                         | b1                      | b2           | 
| ----------------------- | -----------             | -----------  | 
| q1       Value of year  | leap year               | common year  | 
| q2       Value of month | first month of the year | common month |
| q3       Value of day   | first day of the month  | common day   | 
