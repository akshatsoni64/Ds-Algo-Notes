
**Q1- Stock Span Problem**

The span Si of the stock’s price on a given day i is defined as the maximum number of consecutive days just before the given day, for which the price of the stock on the current day is less than or equal to its price on the given day.

For example: {100, 80, 60, 70, 60, 75, 85}
then the span values for corresponding 7 days are {1, 1, 1, 2, 1, 4, 6}.

_Approach 1_ -> Brute Force 

Time Complexity: O(n^2)
Space Complexity: O(1)

_Approach 2_ -> 

If value at arr[i] > arr[i-1], then all the elements in the span of arr[i - 1] will be included in my span, so it makes sense not to make those calculations again. We can simply jump back to that element which was not a part of span of arr[i-1]

```java
tatic void calculateSpan(int price[], int n, int S[]) 
    { 
        // Create a stack and push index of first element to it 
        Stack<Integer> st = new Stack<>(); 
        st.push(0); 
        
        // Span value of first element is always 1 
        S[0] = 1; 
  
        // Pop elements from stack while stack is not empty and top of stack is smaller than price[i] 
        while (!st.empty() && price[st.peek()] <= price[i]) 
          st.pop(); 
  
        // If stack becomes empty, then price[i] is greater than all elements on left of it, i.e., price[0], price[1],               //..price[i-1]. Else price[i] is greater than elements after top of stack 
        S[i] = (st.empty()) ? (i + 1) : (i - st.peek()); 
  
        // Push this element to stack 
        st.push(i); 
        } 
    } 
```
Time Complexity: O(n)
Space Complexity: O(n)

**Q2- Next Greater Element I**
Find the just greater element on right side of each element.
Ex - 4 5 2 25
Ans- 5 25 25 -1

Ex - 10 7 4 2 9 10 11 3 2
Ans- 11 9 9 9 10 11 -1 -1 -1

_Approach 1:_ Use two loops: The outer loop picks all the elements one by one. The inner loop looks for the first greater element for the element picked by the outer loop. If a greater element is found then that element is printed as next element, otherwise -1 is printed.

Time Complexity: O(n^2)
Space Complexity: O(1)

_Approach 2:_
  Intuition:
  In case of a decreasing sequence, the answer is always going to be -1 for all elements till I dont encounter a increasing   sequence/number. 
  For eg: 5 4 3 2 1
          -1 -1 -1 -1 -1
          
          5 4 3 2 1 10
          10 10 10 10 10 -1
          
          For all the elements less than 10 in a decreasing sequence are going to have the answer 10. 
          
          11 4 3 2 10 12
          
          Till 2, it is a decreasing sequence. After that, it is a increasing sequence then. So, for all the elements less             than 10, the elements are going to have an answer 10. 
          Now the question is reduced to 11 10 12. Again 11 and 10 is a decreasing sequence, so the answer for them is going           to be 12 12. 
          
```java
static void printNGE(int arr[], int n)  
    { 
        int i = 0; 
        stack s = new stack(); 
        s.top = -1; 
        int element, next; 
        s.push(arr[0]); 
        for (i = 1; i < n; i++)  
        { 
            next = arr[i]; 
            if (s.isEmpty() == false)  
            {  
                element = s.pop(); 
                while (element < next)  
                { 
                    System.out.println(element + "-->" + next); 
                    if (s.isEmpty() == true) 
                        break; 
                    element = s.pop(); 
                } 
                if (element > next) 
                    s.push(element); 
            } 
            s.push(next); 
        } 
        while (s.isEmpty() == false)  
        { 
            element = s.pop(); 
            next = -1; 
            System.out.println(element + "-->" + next); 
        } 
```
Time Complexity: O(n) 
Space Complexity: O(n)

**Q3- Next Greater Element II**
Consider the case of circular array
Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
```java
public int[] nextGreaterElement(int[] findNums, int[] nums) {
        Stack < Integer > stack = new Stack < > ();
        HashMap < Integer, Integer > map = new HashMap < > ();
        int[] res = new int[findNums.length];
        for (int i = 0; i < nums.length; i++) {
            while (!stack.empty() && nums[i] > stack.peek())
                map.put(stack.pop(), nums[i]);
            stack.push(nums[i]);
        }
        while (!stack.empty())
            map.put(stack.pop(), -1);
        for (int i = 0; i < findNums.length; i++) {
            res[i] = map.get(findNums[i]);
        }
        return res;
    }
```
Time complexity : O(m+n)O(m+n)
Space complexity : O(m+n)O(m+n).

**Q4- Next Greater Element III**

Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. 

Input: [1,2,1]
Output: [2,-1,2]

```java
public int[] nextGreaterElements(int[] nums) {
        int[] res = new int[nums.length];
        Stack<Integer> stack = new Stack<>();
        for (int i = 2 * nums.length - 1; i >= 0; --i) {
            while (!stack.empty() && nums[stack.peek()] <= nums[i % nums.length]) {
                stack.pop();
            }
            res[i % nums.length] = stack.empty() ? -1 : nums[stack.peek()];
            stack.push(i % nums.length);
        }
        return res;
    }
```
Time Complexity: O(n) 
Space Complexity: O(n)

**Q5- Next Smaller Element**

**Q6- Maximum area of a rectangle in a histogram**
Input: 7 bars of heights {6, 2, 5, 4, 5, 1, 6}
Output: Max Area = 12

**Q7- Maximal Rectangle**
**Q8- Remove Duplicates and answer should be lexicographically smallest**

Input: bcabc
Output: abc

Input: cbacdcbc
Output: acdb

**Q9- Decode an encrypted string**


**Q10- Number of Valid Subarrays**
Given an array A of integers, return the number of non-empty continuous subarrays that satisfy the following condition:
The leftmost element of the subarray is not larger than other elements in the subarray.
Input: [1,4,2,5,3]
Output: 11
Explanation: There are 11 valid subarrays: [1],[4],[2],[5],[3],[1,4],[2,5],[1,4,2],[2,5,3],[1,4,2,5],[1,4,2,5,3].
```java 
public int validSubarrays(int[] nums) {
        int res = 0;
        Stack<Integer> stack = new Stack<>();
        for (int num : nums) {
            while (!stack.isEmpty() && num < stack.peek()) {
                stack.pop();
            }
            stack.push(num);
            res += stack.size();
        }
        return res;
    }
```
Time Complexity: O(n) 
Space Complexity: O(n)

**Q11- Miscellaneous Question**