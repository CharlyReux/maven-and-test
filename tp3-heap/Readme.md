This project was very similar to the previous one, I first used input space partitioning to design our first test cases:<br>

The inputs are common to all methods apart from push which takes an element.
 I decided to start by testing the push method so that I could use it for the next tests.
 For this method I considered 4 inputs, the height of the tree, the value of the root, the value of the first childLeft and the value of the first childRight.
 I chose all of these inputs depending on the value of the input "element"
 
|                            | b1                      | b2           | b3           | b4           | 
| -----------------------    | -----------             | -----------  | ------------ |  ---------   |
| q1       Tree's height     | 0                       | 1            | 2            |              |
| q2       root value        | <element                | >element     | =element     |              |
| q3       childLeft value   | <element                | >element     | =element     |              |
| q4       childRightvalue   | <element                | >element     | =element     | null         |

For the pop() method I chose the same input as the push method but i modified the blocks:
|                            | b1                      | b2           | b3           | b4           |  
| -----------------------    | -----------             | -----------  | ------------ |  ---------   |
| q1       Tree's height     | 0                       | 1            | 2            |              |
| q2       root value        | 0                       | 1            |              |              |
| q3       childLeft value   | 0                       | 1            |              |              |
| q4       childRightvalue   | 0                       | 1            |   null       |              |

As for the peek() method I tested with an empty heap and a heap with one element since the ordering was already tested with pop.

And to finish, for the count method I tested with 5 different sizes of tree,{0,1,2,3,4,5} .

I used Jacoco to check the coverage.
The first results I got were 100% on every method except pop(), I have but the screenshot in the code folder of the exercice.

The issue was that I had not tested some code inside a condition, more precisely when the childRigth was the smaller child. The issue that caused this is that I wasn't testing pop on trees with 3 of heigh so the rigthChild just did not exist. I resolved this issue by adding a test with the appropriate tree.:
```java
@Test
	public void testPop3Height0101() {
		MyTreeInputList.add(0);
		MyTreeInputList.add(1);
		MyTreeInputList.add(0);
		MyTreeInputList.add(1);

		myBinHeap.setHeap(MyTreeInputList);
		
		MyTreeTestList.add(0);
		MyTreeTestList.add(1);
		MyTreeTestList.add(1);
		
		assertEquals(myBinHeap.pop(), 0);
		assertEquals(myBinHeap.getHeap(),MyTreeTestList);
	}

```

 After solving this issue, the code was reachable but one branche was still missed in the condition.
```java
if (indexChildRight<heap.size() && comparator.compare(heap.get(indexChildRight), heap.get(indexChildLeft)) <= 0) {
```
But the branch that was missed just could not be reached because if the index of the right child was out of bounds, then the comparator could not get a value out of it.


With the pit report, I got two surviving mutant and both were on conditions similar to the one above.

The first surviving mutant was on this condition, and it survived because changing the boundary condition in here does not change the behavior of the code
```java
if (indexChildRight<heap.size() && comparator.compare(heap.get(indexChildRight), heap.get(indexChildLeft)) <= 0) {
```
The second surviving mutant was on this condition, and it survived because of the same reason as for the other one. The mutant changed the boundary, but this part of the condition was not reached so it did not change the behavior of the code.
```java
if (minChild!=null && comparator.compare(heap.get(currentIndex), minChild) > 0) {
```
