#### Please add your answers to the ***Analysis of  Algorithms*** exercises here.

## Exercise I

a) log(n)
   it runs log(n) times. Since a_1 is 2a_0 + n^2 for each loop, a is growing at rate 2^n - 1
   


b) nlog(n)
   it loops over n, and inside, the loop is log base 2 of n (j grows as 2^n), and has const time ops inside


c) n
   it runs n times (n == bunnies). Effectively a for loop over n with ears += 2 (O(1)) each loop

## Exercise II

Since eggs break easily, just pick floor 0 and be done.
Just kidding.

It sounds a bit like binary search to me:

pick mid (integer div)
test by dropping egg
if egg breaks, pick larger half
if egg doesn't break, pick lower half

repeat process until egg breaks or doesn't, and is 1 higher or lower than
a floor where it does break, respectively

# Pseudocode:

    egg_search(n):
        low = 0
        high = n-1

        highest_didnt_break = 0
        lowest_did_break = n-1

        while lowest_did_break - highest_didnt_break > 1:
            mid = (high - low)//2 + low
            drop at mid

            if egg broke:
                lowest_did_break = mid
                high = mid
            else:
                highest_didnt_break = mid
                low = mid

        return highest_didnt_break

Looks like log(base 2) of n for run times.


# Actual code used to make sure this works:

## arbitrarily made egg break on floors >= 1/3 n
    def drop(val, n):
        if val >= n//3:
            print('break')
            return 1
        else: 
            print('no break')
            return 0

## egg search
    def egg_search(n):
        low = 0
        high = n-1

        hdb = 0
        ldb = n-1


        while ldb - hdb > 1:
            mid = (high - low )//2 + low
            if drop(mid, n):
                ldb = mid
                high = mid
                
            else:
                hdb = mid
                low = mid
        return hdb

    print(egg_search(18))