 --Quiz Funnel
 SELECT question, COUNT(DISTINCT user_id)
 FROM survey
 GROUP BY 1;

-- Question 1 - 100% - 500
-- Question 2 - 95% - 475
-- Question 3 - 80% - 380
-- Question 4 - 95% - 361
-- Question 5 - 75% - 270

-- Question 3, perhaps people do not know different eyeglass shapes and it is a hassle to go learn.
-- Question 5, perhaps it has been a while since the last eye exam and they are embarassed?

--Creating a new table
WITH funnel AS (
SELECT DISTINCT q.user_id, 
  h.user_id IS NOT NULL AS 'is_home_try_on',
  h.number_of_pairs,
  p.user_id IS NOT NULL AS 'is_purchase'
FROM quiz q
LEFT JOIN home_try_on h
  ON q.user_id = h.user_id
LEFT JOIN purchase p
  ON p.user_id = q.user_id
)

--Quiz Funnel
SELECT COUNT(*), SUM(is_home_try_on), SUM(is_purchase)
FROM funnel;

-- 75% of users who completed the quiz tried on the glasses from home. 
-- 66% of users who tried on glasses at home purchased.

WITH funnel AS (
SELECT DISTINCT q.user_id, 
  h.user_id IS NOT NULL AS 'is_home_try_on',
  h.number_of_pairs,
  p.user_id IS NOT NULL AS 'is_purchase'
FROM quiz q
LEFT JOIN home_try_on h
  ON q.user_id = h.user_id
LEFT JOIN purchase p
  ON p.user_id = q.user_id
)
SELECT (1.00 * SUM(is_purchase) / SUM(is_home_try_on))
FROM funnel
WHERE number_of_pairs = "3 pairs";

-- Customers who received 5 pairs had a purchase rate of 79%, and customers who received 3 pairs had a purchase rate of 53%.

SELECT response, COUNT(*)
FROM survey
WHERE question = "3. Which shapes do you like?"
GROUP BY 1
ORDER BY 2 DESC;

--Most popular shapes:
-- Rectangular	141
-- Square	119
-- Round	91
-- No Preference	29

SELECT response, COUNT(*)
FROM survey
WHERE question = "4. Which colors do you like?"
GROUP BY 1
ORDER BY 2 DESC;

-- Most popular colors:
-- Tortoise	117
-- Black	112
-- Crystal	69
-- Neutral	36
-- Two-Tone	27

SELECT response, COUNT(*)
FROM survey
WHERE question = "2. What's your fit?"
GROUP BY 1
ORDER BY 2 DESC;

-- Most popular fits:
-- Narrow	208
-- Medium	132
-- Wide	88
-- I'm not sure. Let's skip it.	47

SELECT response, COUNT(*)
FROM survey
WHERE question = "1. What are you looking for?"
GROUP BY 1
ORDER BY 2 DESC;

-- What are you looking for?
-- Men's Styles	242
-- Women's Styles	209
-- I'm not sure. Let's skip it.	49

SELECT response, COUNT(*)
FROM survey
WHERE question = "4. Which colors do you like?" AND user_id IN (
  SELECT user_id
  FROM survey
  WHERE response = "Women's Styles"
)
GROUP BY 1
ORDER BY 2 DESC;

-- Most popular color among those looking for women's styles:
-- Tortoise	54
-- Black	47
-- Crystal	34
-- Two-Tone	13
-- Neutral	11

SELECT response, COUNT(*)
FROM survey
WHERE question = "4. Which colors do you like?" AND user_id IN (
  SELECT user_id
  FROM survey
  WHERE response = "Men's Styles"
)
GROUP BY 1
ORDER BY 2 DESC;

-- Most popular color among those looking for men's styles:
-- Black	58
-- Tortoise	53
-- Crystal	29
-- Neutral	22
-- Two-Tone	11

SELECT color, COUNT(*)
FROM purchase
GROUP BY 1
ORDER BY 2 DESC;

-- Men's Styles	243
-- Women's Styles	252

-- color	COUNT(*)
-- Jet Black	86
-- Driftwood Fade	63
-- Rosewood Tortoise	62
-- Rose Crystal	54
-- Layered Tortoise Matte	52
-- Pearled Tortoise	50
-- Elderflower Crystal	44
-- Sea Glass Gray	43
-- Endangered Tortoise	41
