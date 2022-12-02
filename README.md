# Advent of code 2022, in Stax

[Stax](https://github.com/tomtheisen/stax/tree/master/docs#stax) is a [code golfing](https://en.wikipedia.org/wiki/Code_golf) language, which means it is designed to be used to solve problems in as few bytes as possible.
I haven't tried code golfing before and Stax seemed to be somewhat intuitive.
This repo will document be as far as I can go, using Stax - not necessarily opting for the most efficient, or smallest programs - just whatever I can do that works.

You can try these solutions yourself by visiting this [http://stax.tomtheisen.com/](http://stax.tomtheisen.com/)

Thanks to https://stackedit.io/app# for making this writeup easier

## Stats so far:
Challenges completed: 4

Bytes used: 85

Average bytes to solve: 21.25

## Day 1a
#### Code (16 bytes)
    _|j{!}/2::{{em|+m|M
    Packed:
    ì╜E↓É║¥▐E&X°σ·┐·

#### Explanation
    _           Load all the input as a string/array
     |j     	Split the string by newlines
       {!}/ 	Group contiguous elements by falsy values
       2::  	Remove all even sets (they are empty)
       {    	For each valid group
         {em	Parse each number in the nested array
         |+ 	Sum them
       m		Map all the sums
       |M		Find the Maximum


## Day 1b
#### Code (25 bytes)
    _|j{!}/2::{{em|+m3{dc|MX|-xm|+
    Packed:
    äO£♠¼ï╨Ç♥4┤3æÅXD⌐╥0░ªx4D4

#### Explanation
    _           	Load all the input as a string/array
     |j     		Split the string by newlines
       {!}/ 		Group contiguous elements by falsy values
       2::  		Remove all even sets (they are empty)
       {    		For each valid group
         {em		Parse each number in the nested array
         |+ 		Sum them
       m			Map all the sums
       3{			Create a range of [1..3]
         dc			Discard the index, and copy the current sum
         |M			Find the max value in the array
         X			Store the max value in register X
         |-			Pop the max value from the array
         x			Recall the max value from register X
       m			Complete Mapping of [1..3] to the maxes
       |+			Sum the three maxes



## Day 2a
#### Code (22 bytes)
    _|j{Esdc87-Xd-3%3*6s-x+m|+
    Packed:
    ÇπQ∞a,W╩δC╙├╩Q╕┴≥T:α!≡

#### Explanation
    _           	Load all the input as a string/array
     |j     		Split the string by newlines
       {			Begin mapping each string
         E			Explode out the characters into the stack
         sdc		Swap the last two characters, discard the space, and copy it
         87-		Subtract 87 (W) from the last character to get points
         X			Store the points for picking the option into X
         d			Discard the points for now
         -			Subtract our option from their option
         3%			Abs modulus the result by 3 (now 0-2 range)
         3*			Multiply the result by 3 (0-6 range)
         6s-		Perform 6 - the result to align it to get result points
         x			Recall the points for picking the option
         +			Add them together
       m			Complete mapping input line to score
       |+			Sum all the row scores


## Day 2b
#### Code (22 bytes)
    _|j{Esd88-c3*sa63-+3%1++m|+
    Packed:
    ╘[fHf6¢=/9»╡→┬╤▄ö╫░we;

#### Explanation
    _           	Load all the input as a string/array
     |j     		Split the string by newlines
       {			Begin mapping each string
         E			Explode out the characters into the stack
         sdc		Swap the last two characters, discard the space, and copy it
         88-		Subtract 88 (X) from the last character to get our result
         c			Copy the result as we will use it later to determine our pick
         3*			Multiply the result by 3 to get our result points
         sa			Flip the top 3 elements on the stack
         63-		Get the option that beats what they played.
         +			Add the expected result to the pick to get what we must play
         3%			Wrap into the 0-2 range
         1+			Add 1 because the score for picking is 1-3
         +			Add the scores of the result and the pick
       m			Complete mapping input line to score
       |+			Sum all the row scores
