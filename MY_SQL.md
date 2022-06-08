<h1 align='center'>MySQL Codes</h1>

<h2>Revising the Select Query</h2>

```SQL
SELECT *
FROM CITY
WHERE POPULATION>=100000 AND COUNTRYCODE = "USA"
```

<h2>Revising the Select Query II</h2>

```SQL
SELECT NAME
FROM CITY
WHERE POPULATION>120000 AND COUNTRYCODE = "USA"
```

<h2>Select All</h2>

```SQL
SELECT *
FROM CITY
```

<h2>Select By ID</h2>

```SQL
SELECT *
FROM CITY
WHERE ID = 1661
```

<h2>Japanese Cities' Attributes</h2>

```SQL
SELECT *
FROM CITY
WHERE COUNTRYCODE = "JPN"
```

<h2>Japanese Cities' Names</h2>

```SQL
SELECT NAME
FROM CITY
WHERE COUNTRYCODE = "JPN"
```

<h2>Weather Observation Station 1</h2>

```SQL
SELECT CITY, STATE
FROM STATION
```

<h2>Weather Observation Station 3</h2>

```SQL
SELECT DISTINCT CITY FROM STATION
WHERE ID%2 = 0
```

<h2>Weather Observation Station 4</h2>

```SQL
SELECT COUNT(CITY) - COUNT(DISTINCT CITY)
FROM STATION
```

<h2>Weather Observation Station 5</h2>

```SQL
SELECT CITY, CHAR_LENGTH(CITY) AS LEN_GTH FROM STATION
WHERE CITY REGEXP 'a[a-z]|b[a-z]' AND CHAR_LENGTH(CITY) > 20 OR CITY = "AMO"
ORDER BY LEN_GTH DESC
```

<h2>Weather Observation Station 6</h2>

```SQL
SELECT DISTINCT CITY FROM STATION
WHERE CITY REGEXP "^a|^e|^i|^o|^u"
```

<h2>Weather Observation Station 7</h2>

```SQL
SELECT DISTINCT CITY FROM STATION
WHERE CITY REGEXP "a$|e$|i$|o$|u$"
```

<h2>Weather Observation Station 8</h2>

```SQL
SELECT DISTINCT CITY FROM STATION
WHERE CITY REGEXP "^[aeiou]" AND CITY REGEXP "[aeiou]$";
```

<h2>Weather Observation Station 9</h2>

```SQL
SELECT DISTINCT CITY FROM STATION
WHERE CITY not REGEXP "^[aeiou]"
```

<h2>Weather Observation Station 10</h2>

```SQL
SELECT DISTINCT CITY FROM STATION
WHERE CITY NOT REGEXP "[aeiou]$"
```

<h2>Weather Observation Station 11</h2>

```SQL
SELECT DISTINCT CITY FROM STATION 
-- WHERE CITY NOT REGEXP "^[aeiou]" and CITY NOT REGEXP "[aeiou]$" THIS IS ALSO CORRECT BUT IT IS NOT TAKING


WHERE LEFT(CITY, 1) NOT IN ('A', 'E', 'I', 'O', 'U') OR RIGHT(CITY, 1) NOT IN ('a', 'e', 'i', 'o', 'u')
```

<h2>Weather Observation Station 12</h2>

```SQL
SELECT DISTINCT CITY FROM STATION
where city not REGEXP "^[aeiou]" and city not regexp "[aeiou]$"

-- WHERE LEFT(CITY, 1) NOT IN ('A', 'E', 'I', 'O', 'U') OR RIGHT(CITY, 1) NOT IN ('a', 'e', 'i', 'o', 'u')
```
