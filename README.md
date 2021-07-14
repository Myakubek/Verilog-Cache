# Verilog-Cache
  * [Direct Mapped](#direct-mapped)
  * [Two-set Associative](#two-set-associative)
  * [Fully Associative](#fully-associative)
  * [Outputs](#outputs)

These programs implements a cache (in 4 & 8 element versions) configured as direct mapped, two-way set associative, and fully associative. Each element is aa four-bit memory address.
The program reads a trace file of 100 values from memory ranging from 1-15 and inserts the items into the cache, the program will count the hits and misses and return the total for each cache mapping approach. 

## Direct Mapped

The two tables below model the indexes, tags, and addresses that the program will work with. This version of cache mapping spreads out values in cache memory to minimize misses. This solution does so by defining tags and indexes which correlate to inputs, therefore we only need to keep track of what value is stored in cache and whether or not a miss or hit occurs. The general flow of the program is:  

1. Based on the input 1-15 set the tag and index accordingly  
2. Check the correlated index and see if the tag matches  
   1. If the tag is there return a hit  
   2. If the tag is not there, return a miss and store the tag in the index. 

In an eight-element cache:  
Because we have double the indexes and the same amount of addresses to map, fewer addresses map to the same index resulting in substantially less misses.  

![alt text](https://github.com/Myakubek/Verilog-Cache/blob/main/Images/4%20Cache%20-%20Direct%20Map.png?raw=true)  



![alt text](https://github.com/Myakubek/Verilog-Cache/blob/main/Images/8%20Cache%20-%20Direct%20Map.png?raw=true) 

## Two-set Associative

In #-set associative mapping, the cache is divided into groups (two in this case). Data is mapped into one set, and then placed into blocks within the set. The program also uses an LRU mechanism to determine which index needs to be replaced. Inputs will be assigned an index that represents a set instead of a specific location, and they will still have distinct tags based on their index. The general flow of the program is:

1. Given input, assign the corresponding tag and index based on the set.
2. Check all locations within the set to see if the tag is already stored
   1. If a matching tag is found, then replace the tag and update the LRU
   2. if there is no matching tag, then replace the location designated by the LRU, and update the LRU with the new input.

In an eight element cache:

The general flow remains the same, however, each LRU needs to span 4 elements instead of 2.


![alt text](https://github.com/Myakubek/Verilog-Cache/blob/main/Images/4%20Cache%20-%20Two%20set.png?raw=true) 

![alt text](https://github.com/Myakubek/Verilog-Cache/blob/main/Images/8%20Cache%20-%20Two%20Set.png?raw=true) 

## Fully Associative

For fully associative mapping, we don't care about index values since any value can map to any location in the cache. Fully associative mapping focuses heavily on an LRU that spans all indexes in the cache. This means all tags need to be distinct value based on inputs, which allows the use of their binary values as the index. The general flow of the program is:

1. set LRU to default values
2. Given an input, check through the cache based on the LRU to see if there's a hit or a miss
   1. If there's a hit store the location in cache, and update the LRU to move the location to the front of the LRU.
   2. If there's a miss, store the value at the index stored at the back of the LRU and update the values in cache and the LRU values. 


![alt text](https://github.com/Myakubek/Verilog-Cache/blob/main/Images/4%20Cache%20-%20Fully%20Assoc.png?raw=true) 


![alt text](https://github.com/Myakubek/Verilog-Cache/blob/main/Images/8%20Cache%20-%20Fully%20Assoc.png?raw=true) 

## Outputs

The outputs show the total misses and hits given the input file (trace) following the different forms of cache mapping. The four element cache output displays a debug stream of line-by-line result of the hits and misses as they are being read into the program.

![alt text](https://github.com/Myakubek/Verilog-Cache/blob/main/Images/4%20Cache%20-%20Output.png?raw=true) 

![alt text](https://github.com/Myakubek/Verilog-Cache/blob/main/Images/8%20Cache%20-%20Output.png?raw=true) 
