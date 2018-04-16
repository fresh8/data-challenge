# data-challenge
The technical challenge for the Data Engineer role at Fresh8

## Background

The challenge is broken down into 3 separate parts which are aimed to test a number of technical abilities that we expect data engineers to possess at Fresh8.

There are 3 types of events:

`Viewed` - An advert was viewed
`Interacted` - An advert was interacted with (but not clicked through)
`Clicked-through` - An used clicked out of the ad to the product

## Rules

* You will be provided with a dump of sanitsed data
* Use any technologies you want but be able to justify it
* Keep detailed records of your findings and approach so we can discuss it during the technical interview

## PART 1

Analyse the dataset and determine the top 5 Browsers, Operating Systems and Cities and visualise the data so that it can be interpreted.
Consider that you will need to enrich this data to achieve the goal.

## PART 2

Create the following user funnels:

`Viewed > Interfacted > Clicked-Through`

and

`Viewed > Clicked-Through`

What conclusions can we draw by interpreting these results, if at all.

## PART 3

Build probabilistic models using the data set to predict the likelihood that someone would click on one of the adverts.

What is the likelihood that someone:

* in London who uses Chrome will Interact with of the adverts?
* a Mobile user in Manchester clicks on a Horse Racing bet?
* What other interesting conclusions could you draw?
