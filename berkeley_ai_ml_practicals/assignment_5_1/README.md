# Will a Customer Accept the Coupon?

# Problem Statement 

Imagine driving through town and a coupon is delivered to your cell phone for a restaraunt near where you are driving. Would you accept that coupon and take a short detour to the restaraunt? Would you accept the coupon but use it on a sunbsequent trip? Would you ignore the coupon entirely? What if the coupon was for a bar instead of a restaraunt? What about a coffee house? Would you accept a bar coupon with a minor passenger in the car? What about if it was just you and your partner in the car? Would weather impact the rate of acceptance? What about the time of day?

Obviously, proximity to the business is a factor on whether the coupon is delivered to the driver or not, but what are the factors that determine whether a driver accepts the coupon once it is delivered to them? How would you determine whether a driver is likely to accept a coupon?

### Overview

The goal of this project is to use what you know about visualizations and probability distributions to distinguish between customers who accepted a driving coupon versus those that did not.

### Data

This data comes to us from the UCI Machine Learning repository and was collected via a survey on Amazon Mechanical Turk. The survey describes different driving scenarios including the destination, current time, weather, passenger, etc., and then ask the person whether he will accept the coupon if he is the driver. Answers that the user will drive there ‘right away’ or ‘later before the coupon expires’ are labeled as ‘Y = 1’ and answers ‘no, I do not want the coupon’ are labeled as ‘Y = 0’. There are five different types of coupons -- less expensive restaurants (under $20), coffee houses, carry out & take away, bar, and more expensive restaurants ($20 - $50).

# Observations and Conclusions

## Observations
- The overall Acceptance rate for any coupon is = 43.16% 
- The overall Acceptance rate for a Bar coupon is = 41.00% Acceptance rate across
- Acceptance rate for those who go to a bar 3 or more times = 19%
- Acceptance rate for those who go to bar more than once a month and are over the age of 25 = 14.58%
- Acceptance rate for those who go to bar more than once a month and had passengers that were not a kid and had occupations other than farming, fishing, or forestry = 71.79%
- Acceptance rate for those who are young and single starting their career(lower income) - 59%

## Conclusions
- Overall the bar coupons acceptance rates is on par with other types of coupons
- The worst category to target would be individuals who frequent bar more often.
- Having a kid in the car is a deterrent to accepting the Coupon. Which is great, shows the drivers are responsible

## Futher invetigation Required
- Does the length of the day determine if the bar coupon is accepted. Example, it gets darker earlier in the day in winters, will this influence people to accept the coupon
- Expiration duration - if the coupon has a longer expiration duration is the acceptance rate higher. Example, if the coupon had a 24hour expiration and if I am driving with a child in the car, I would still accept it but go to the bar later after dropping off my kid

## Not enough Data
- Value and type of the bar coupon. Example a "buy 1 get and 1 drink free" might perform better then "10% off a drink"