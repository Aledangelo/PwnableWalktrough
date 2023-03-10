# Lotto

## Solution
The challenge consists in guessing 6 randomly generated numbers from /dev/urandom.
Reading the lotto.c file I noticed two important things:
* Number range is from 1 to 46
```
for(i=0; i<6; i++){
	lotto[i] = (lotto[i] % 45) + 1;		// 1 ~ 45
}
```
* There is an error in the programming logic
```
// calculate lotto score
int match = 0, j = 0;
for(i=0; i<6; i++){
	for(j=0; j<6; j++){
		if(lotto[i] == submit[j]){
			match++;
		}
	}
}
```
The following code is used to check if the 6 numbers entered in input are equal to the numbers generated by urandom.

Notice something strange? Each number in the first array is compared to each number of the second array. If there are two equal numbers, a counter is increased by 1.

If the counter, at the end, is equal to 6 you win.
```
// win
if(match == 6){
	system("/bin/cat flag");
}
else{
	printf("bad luck...\n");
}
```
To increase the counter up to 6, we just need to input six equal numbers, if one of the random numbers is equal to those inserted in input then the counter will be increased 6 times.

The probability of guessing a number in the range of numbers between 1 and 46 is about 2%, having 6 numbers available the probability increases to 13%. It's not much, but it can be fine :)

With at least a hundred attempts we should be able to read the flag. I wrote a python script that sends the string made up of 6 equal bytes as input repeatedly until the flag is printed on the screen.

## Usage
```
python3 exploit.py /home/lotto
```
