## 3. SELECT From Nobel
![](images/SELECT_from_Nobel_pic_1.png)

1.Change the query shown so that it displays Nobel prizes for 1950.
```sql
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950;
```

2.Show who won the 1962 prize for Literature.
```sql
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'Literature';
```

3.Show the year and subject that won 'Albert Einstein' his prize.
```sql
SELECT yr, subject
FROM nobel
WHERE winner LIKE 'Albert Einstein';
```

4.Give the name of the 'Peace' winners since the year 2000, including 2000.
```sql
SELECT winner
FROM nobel
WHERE subject='Peace' AND yr >= 2000;
```

5.Show all details (yr, subject, winner) of the Literature prize winners for 1980 to 1989 inclusive.
```sql
SELECT yr, subject, winner
FROM nobel
WHERE subject LIKE 'Literature' AND (yr >= 1980 AND yr <= 1989);
```

6.Show all details of the presidential winners:
Theodore Roosevelt
Woodrow Wilson
Jimmy Carter
Barack Obama
```sql
SELECT * FROM nobel
 WHERE winner IN ('Theodore Roosevelt',
                  'Woodrow Wilson',
                  'Jimmy Carter',
                  'Barack Obama');
```

7.Show the winners with first name John
```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%';
```

8.Show the year, subject, and name of Physics winners for 1980 together with the Chemistry winners for 1984.
```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject LIKE 'Physics' AND yr=1980) OR (subject LIKE 'Chemistry' AND yr=1984);
```

9.Show the year, subject, and name of winners for 1980 excluding Chemistry and Medicine
```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr=1980 AND subject NOT LIKE 'Chemistry' AND subject NOT LIKE 'Medicine';
```

10.Show year, subject, and name of people who won a 'Medicine' prize in an early
year (before 1910, not including 1910) together with winners of a 'Literature' prize
in a later year (after 2004, including 2004)
```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject LIKE 'Medicine' AND yr < 1910)
  OR (subject LIKE 'Literature' AND yr >= 2004);
```

11.Find all details of the prize won by PETER GRÜNBERG
```sql
SELECT *
FROM nobel
WHERE winner = CONCAT('PETER GR', CHAR(252), 'NBERG');
```

12.Find all details of the prize won by EUGENE O'NEILL
Escaping single quotes
```sql
SELECT *
FROM nobel
WHERE winner = concat('EUGENE O', CHR(39), 'NEILL');
```

13.Knights in order
List the winners, year and subject where the winner starts with Sir.
Show the the most recent first, then by name order.
```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%' ORDER BY yr DESC, winner;
```

14.The expression subject IN ('Chemistry','Physics') can be used as a value - it will be 0 or 1.
Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.
```sql
SELECT winner, subject
  FROM nobel
 WHERE yr=1984
 ORDER BY subject IN ('Physics','Chemistry'), subject, winner;
```