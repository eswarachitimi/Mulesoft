
Just an FYI … This is collated from various internet articles … Please feel free to add/update to this table  …


Function	Works on	$	$$	$$$	Works on Null
map	Arrays Only	Value	Index	N/A	Yes
mapObject	Objects Only	Value	Key	Index	Yes
pluck	Objects Only	Value	Key	Index	No
filter	Arrays & Objects	Value	Index on Array, Key on Object	On Objects, it is documented that this is Index, though when tested this currently does not work. 
However, when using named parameters, this third parameter works.	Yes
orderBy	Arrays & Objects	Value	Index on Array, Key on Object	N/A	No
distinctBy	Arrays & Objects	Value	Index on Array, Key on Object	N/A	No
groupBy	Arrays & Objects	Value	Index on Array, Key on Object	On Objects, it is documented that this is Index, though when tested this currently does not work. 
However, when using named parameters, this third parameter works	No
reduce	Arrays Only	Value	Accumulator	N/A	No
match	 	Input Expression	 	 	 
replace	 	All matches of the given expression 
(match string + capture groups)	Index of the regex match	 	 


Example,
•	payload filter (value, index) -> value.id > 123  
can be expressed as below using lambda
•	payload filter $.id > 123

