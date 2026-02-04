Tools: MySQL, MySQL Connector, Power BI  <br>
Scroll further down for MySQL codes.  <br>
Data is sourced from AbsentData.com.  <br>

Data for the revenue of a certain hotel brand was taken from 2019, 2019, and 2020, providing revenue and reservation information from those three years for both City Hotel and Resort Hotel. Data has been slightly pre-cleaned and then split into separate workbooks to allow work on MySQL. Through MySQL, a new CTE table was created and is connected with MySQL Connector to allow data visualization on Power BI. There's over 100k rows combined from all three years of data. <br>

In Power BI, data is transformed and adjusted, particularly the date to ensure they reflect correct formatting for easy data visualization. <br>
There are three main questions we're seeking through this data: **Is the revenue growing? Do we need to add parking spaces? And if there's any trend we should be noticing?** <br>
1. **Revenue dropped significantly during Q4 of 2019** and is slowly picking back up as 2020 continues. As this is the pandemic, it's highly unlikely for sales to continue to grow back to its previous 2019 peak during Q3 anytime soon. There's a need for temporary measures to ensure hotel can maintain its current profit from declining and to weather the upcoming possible crisis.
2. **Parking space is currently more than sufficient** and despite reservations picking back up in 2020. It may take a while until there's a need to increase parking space, which should also be done in conjunction with the increase of room capacity when social distancing and travel bans loosens.
3. Trends:
   - **Resort Hotel** is trending upward as reservations are picking back up.
   - More reservations are made from **Online TA** and less are made offline.
   - **Corporate bookings** show more repeated guests than any other types of bookings.

<img width="1547" height="806" alt="image" src="https://github.com/user-attachments/assets/e21c3e97-b41b-4042-8ec4-2af417cd7333" />


Based on the data and the significantly unique climate of this time range, some actions to consider:
1. Travel ban means marketing to customers that are not allowed to leave or visit the country should be lessened.
2. On the flip side, market to locals or countries where travel bans have loosened up. Offer discounts and other facilities to cut losses.
3. No need for unnecessary expenditure such as increasing parking space.
4. With Corporate and Group reservations showing the most consistent figures, increase their brand loyalty and appeal.


MySQL code: <br>
```WITH HotelRevs as
(
	SELECT *
	FROM rev_2018
	UNION
	SELECT *
	FROM rev_2019
	UNION
	SELECT *
	FROM rev_2020
	)
SELECT market_segment, adr, reserved_room_type
FROM HotelRevs;

WITH HotelRevs as
(
	SELECT *
	FROM rev_2018
	UNION
	SELECT *
	FROM rev_2019
	UNION
	SELECT *
	FROM rev_2020
	)
SELECT
	arrival_date_year AS `Year`, hotel,
	SUM(stays_in_weekend_nights + stays_in_week_nights) AS StayLength,
    ROUND(SUM((stays_in_weekend_nights + stays_in_week_nights) * adr)) AS TotRev
FROM HotelRevs
WHERE is_canceled = 0
GROUP By arrival_date_year, hotel
;

WITH HotelRevswithDiscount as
(
	WITH HotelRevs as
    (
		SELECT *
		FROM rev_2018
		UNION
		SELECT *
		FROM rev_2019
		UNION
		SELECT *
		FROM rev_2020
		)
SELECT *
FROM HotelRevs
LEFT JOIN marketsegment
	USING(market_segment)
    )
SELECT
	country,
	market_segment,
    arrival_date_year,
    ROUND(SUM((stays_in_weekend_nights + stays_in_week_nights) * adr)) AS TotRev
FROM HotelRevswithDiscount
WHERE is_canceled = 0
GROUP BY arrival_date_year, market_segment, country
;

WITH RevsMarketMeal as
(
	WITH RevsAndMarket as
	(
		WITH HotelRevs as
		(
			SELECT *
			FROM rev_2018
			UNION
			SELECT *
			FROM rev_2019
			UNION
			SELECT *
			FROM rev_2020
		)
	SELECT *
	FROM HotelRevs
	LEFT JOIN marketsegment
		USING(market_segment)
	)
	SELECT *
    FROM RevsAndMarket
    LEFT JOIN meal_cost
		USING(meal)
)
SELECT *
FROM RevsMarketMeal
;

SELECT *
FROM meal_cost;
```
