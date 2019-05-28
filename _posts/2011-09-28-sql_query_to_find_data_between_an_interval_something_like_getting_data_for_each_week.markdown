---
layout: post
title: sql query to find data between an interval.. something like getting data for
  each week
date: '2011-09-28 21:59:00'
---

SELECT MAX( STR_TO_DATE( CONVERT( `PurchaseDt`

USING utf8 ) , '%m-%d-%Y' ) ) AS maxdate, MIN( STR_TO_DATE( CONVERT( `PurchaseDt`

USING utf8 ) , '%m-%d-%Y' ) ) AS mindate

FROM `MemberEarnings`

WHERE STR_TO_DATE( CONVERT( `PurchaseDt`

USING utf8 ) , '%m-%d-%Y' )

BETWEEN STR_TO_DATE( '08-01-2011', '%m-%d-%Y' )

AND STR_TO_DATE( '08-21-2011', '%m-%d-%Y' )

GROUP BY DATE_SUB( STR_TO_DATE( CONVERT( `PurchaseDt`

USING utf8 ) , '%m-%d-%Y' ) , INTERVAL DAYOFWEEK( STR_TO_DATE( CONVERT( `PurchaseDt`

USING utf8 ) , '%m-%d-%Y' ) ) -1

DAY )