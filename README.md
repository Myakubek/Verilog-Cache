# Verilog-Cache
These programs implements a cache (in 4 & 8 element versions) configured as direct mapped, two-way set associative, and fully associative. Each element is aa four-bit memory address.
The program reads a trace file of 100 values from memory ranging from 1-15 and inserts the items into the cache, the program will count the hits and misses and return the total for each cache mapping approach. 

## Direct Mapped
The two tables below model the indexes, tags, and addresses that the program will work with. This version of cache mapping spreads out values in cache memory to minimize misses. This solution does so by defining tags and indexes which correlate to inputs, therefore we only need to keep track of what value is stored in cache and whether or not a miss or hit occurs. The general flow of the program is:  

1. Based on the input 1-15 set the tag and index accordingly  
2. Check the correlated index and see if the tag matches  
3. If the tag is there return a hit  
4. If the tag is not there, return a miss and store the tag in the index.  

### Four-Element
![alt text](https://github.com/Myakubek/Verilog-Cache/blob/main/Images/4%20Cache%20-%20Direct%20Map.png?raw=true) 

In an eight-element cache:  
Because we have double the indexes and the same amount of addresses to map, fewer addresses map to the same index resulting in substantially less misses.  

### Eight-Element
![alt text](https://github.com/Myakubek/Verilog-Cache/blob/main/Images/8%20Cache%20-%20Direct%20Map.png?raw=true) 
