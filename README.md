
# Advent of code 2022, in Stax

[Stax](https://github.com/tomtheisen/stax/tree/master/docs#stax) is a [code golfing](https://en.wikipedia.org/wiki/Code_golf) language, which means it is designed to be used to solve problems in as few bytes as possible.
I haven't tried code golfing before and Stax seemed to be somewhat intuitive.
This repo will document as far as I can go, using Stax - not necessarily opting for the most efficient, or smallest programs - just whatever I can do that works.

You can try these solutions yourself by visiting this [http://stax.tomtheisen.com/](http://stax.tomtheisen.com/)

Thanks to https://stackedit.io/app# for making this writeup easier

## Stats so far:
Challenges completed: 8

Bytes used: 177

Average bytes to solve: 22.125

## Day 1a
#### Code (16 bytes)
    _|j{!}/2::{{em|+m|M
    Packed:
    ì╜E↓É║¥▐E&X°σ·┐·

#### Explanation
    _	Load all the input as a string/array
    |j	Split the string by newlines
    {!}/	Group contiguous elements by falsy values
    2::	Remove all even sets (they are empty)
    {    	For each valid group
      {em	Parse each number in the nested array
      |+ 	Sum them
    m	Map all the sums
    |M	Find the Maximum


## Day 1b
#### Code (25 bytes)
    _|j{!}/2::{{em|+m3{dc|MX|-xm|+
    Packed:
    äO£♠¼ï╨Ç♥4┤3æÅXD⌐╥0░ªx4D4

#### Explanation
    _		Load all the input as a string/array
    |j     		Split the string by newlines
    {!}/ 		Group contiguous elements by falsy values
    2::  		Remove all even sets (they are empty)
    {    		For each valid group
      {em		Parse each number in the nested array
      |+ 		Sum them
    m		Map all the sums
    3{		Create a range of [1..3]
      dc		Discard the index, and copy the current sum
      |M		Find the max value in the array
      X		Store the max value in register X
      |-		Pop the max value from the array
      x		Recall the max value from register X
    m		Complete Mapping of [1..3] to the maxes
    |+		Sum the three maxes



## Day 2a
#### Code (22 bytes)
    _|j{Esdc87-Xd-3%3*6s-x+m|+
    Packed:
    ÇπQ∞a,W╩δC╙├╩Q╕┴≥T:α!≡

#### Explanation
    _		Load all the input as a string/array
    |j     		Split the string by newlines
    {		Begin mapping each string
      E		Explode out the characters into the stack
      sdc		Swap the last two characters, discard the space, and copy it
      87-		Subtract 87 (W) from the last character to get points
      X		Store the points for picking the option into X
      d		Discard the points for now
      -		Subtract our option from their option
      3%		Abs modulus the result by 3 (now 0-2 range)
      3*		Multiply the result by 3 (0-6 range)
      6s-		Perform 6 - the result to align it to get result points
      x		Recall the points for picking the option
      +		Add them together
    m		Complete mapping input line to score
    |+		Sum all the row scores


## Day 2b
#### Code (22 bytes)
    _|j{Esd88-c3*sa63-+3%^+m|+
    Packed:
    ÇπQδ√+¥⌐¶úîô╖╪╙ÿ9▐∞Iüí

#### Explanation
    _		Load all the input as a string/array
    |j     		Split the string by newlines
    {		Begin mapping each string
      E		Explode out the characters into the stack
      sdc		Swap the last two characters, discard the space, and copy it
      88-		Subtract 88 (X) from the last character to get our result
      c		Copy the result as we will use it later to determine our pick
      3*		Multiply the result by 3 to get our result points
      sa		Flip the top 3 elements on the stack
      63-		Get the option that beats what they played.
      +		Add the expected result to the pick to get what we must play
      3%		Wrap into the 0-2 range
      ^		Add 1 because the score for picking is 1-3
      +		Add the scores of the result and the pick
    m		Complete mapping input line to score
    |+		Sum all the row scores


## Day 3a
#### Code (15 bytes)
    _|j{2ME|&hVlsI^m|+
    Packed:
    ëÑ♫♣Wü>âΓ+(¶┐╪┤

#### Explanation
    _		Load all the input as a string/array
    |j     		Split the string by newlines
    {		Begin mapping each string
      2M		Split array into 2 groups
      E		Explode the array onto the stack
      |&		Find the intersection of the arrays
      h		Get the first element (distincting)
      Vl		Load in a-z..A-Z
      s		Swap the elements on the stack
      I		Find the index of our distinct intersection in V1
      ^		Add one because priority is 1-indexed
    m		Complete mapping input line to priority
    |+		Sum all the priorities


## Day 3b
#### Code (17 bytes)
    _|j3/{E|&|&hVlsI^m|+
    Packed:
    üT♥╙JQπ\τeä~█▒≤7╡

#### Explanation
    _		Load all the input as a string/array
    |j     		Split the string by newlines
    3/		Divide array into groups of 3
    {		Begin mapping each array of strings
      E		Explode the array of 3 strings onto the stack
      |&|&		Find the intersection of bags C, B, and A
      h		Get the first element (distincting)
      Vl		Load in a-z..A-Z
      s		Swap the elements on the stack
      I		Find the index of our distinct intersection in V1
      ^		Add one because priority is 1-indexed
    m		Complete mapping arrays of strings to priority
    |+		Sum all the priorities



## Day 4a
#### Code (33 bytes)
    _|j{',/{'-/m:f{em2/{E^|rmc{%m|MsE|L%=m|+
    Packed:
    ì■•└L|û⌂Ü╢σ}T«î]£Iï%╝○IëbH│ÅµSΩRâ

#### Explanation
    _		Load all the input as a string/array
    |j     		Split the string by newlines
    3/		Divide array into groups of 3
    {		Begin mapping each array of strings
      ',/		Create a ',' and split the string on it
      {'-/m         Map each string, create a '-' and split on it
      :f            Flatten the array back to 1 deep
      {em           Convert all strings to numbers
      2/            Split array into 2 equal-size arrays ([2][2])
      {             For each array
        E^          Extract the elements to the stack, increment the 2nd number
        |r          Create a range
      m             Complete mapping the arrays to ranges
      c		Clone the ranges
      {%m           Map the ranges to the lengths of the ranges
      |M            Find the size of the biggest range
      s             Swap the copied range back up
      E             Explode the two range arrays onto the stack
      |L            Union the two ranges
      %=            Check if the size of the union is equal to the largest range
    m               Complete mapping input line, to truthy (0,1)
    |+              Count the lines that were truthy


## Day 4b
#### Code (27 bytes)
    _|j{',/{'-/m:f{em2/{E^|rmE|&!!m|+
    Packed:
    ╕e┌j1îô═∩æ▬⌠jN⌡▌►c|ùíC=α9═☺

#### Explanation
    _		Load all the input as a string/array
    |j     		Split the string by newlines
    3/		Divide array into groups of 3
    {		Begin mapping each array of strings
      ',/		Create a ',' and split the string on it
      {'-/m         Map each string, create a '-' and split on it
      :f            Flatten the array back to 1 deep
      {em           Convert all strings to numbers
      2/            Split array into 2 equal-size arrays ([2][2])
      {             For each array
        E^          Extract the elements to the stack, increment the 2nd number
        |r          Create a range
      m             Complete mapping the arrays to ranges
      E             Extract the elements to the stack
      |&            Intersect the two ranges
      !!            Is the result truthy (0,1)
    m		Complete mapping arrays of strings to truthy (0,1)
    |+		Count the lines that were truthy


## Day 5a
#### Code (61 bytes)
    _"`1`1"/Es|j{D4::mM{tmXs|j{jr2::{evmE^{dbYdxy0@xyxy@D&XaY@+xya&XdFddFx{hm
    Packed:
    Ç₧┬╜W╟h<PΘ▓♥£4╩ⁿ=%┌≤┬☺eX»%6■T◘╕╝²ùτüΓτ~◙σ¿Ω4█▒╠¬╞τmEº≤♥☺╟¥Ωía

#### Explanation (coming soon)
    _"`1`1"/
    E
    s
    |j
    {D4::m
    M
    {tm
    X
    s
    |j
    {
      j
      r
      2::
      {evm
      E
      ^
      {
        db
        Yd
        xy0@
        xy
        xy@
        D
    &

    X
    aY@
    +
    
    xya&
    X
    d
      F
      dd
    F
    x
    {hm


