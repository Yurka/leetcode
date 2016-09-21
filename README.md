# loop through leetcode one more time, ; )
* [strategy](#strategy)
* [practice patterns](#practice-pattern)
* [communication patterns](#communication-pattern)
* [questions to confirm about input](#input-specification)
* [java collections internals](#java-collections)
* [summarized code snippets](#snippets)
	* [Java basic apis](#basic-apis)
	* [math](#math)
	* [array](#array)
	* [string](#string)
	* [linkedlist](#linkedlist)
	* [sort](#sort)
	* [binary-search](#binary-search)
	* [stack](#stack)
	* [queue/priorityqueue](#queue)
	* [hashtable](#hashtable)
	* [recursive functions](#recursive)
	* [enumeration](#enumeration)
	* [depth first search](#dfs)
	* [breath first search](#bfs)
	* [graph](#graph)
	* [Trie](#trie)
	* [dynamic-programming](#dynamic-programming)
* [error-prone cases](#error-prone)
* [smells for refactoring and optimization](#bad-smells)
* [Java sins](#java-sins)
* [leetcode sins](#leetcode-sins)

### Strategy <a id="strategy"></a>
* Think from perspectives of designing products and teamwork
  * Think as if you are desigining product
    * identify problems
    * make tradeoffs
    * attention to details
    * be passionate
  * Think as if you are talking to your teammates
    * be a logical person, optimize from brute force to best
    * speak out your thoughts for discussion when stuck
    * be humble, always quick to take ideas from others
* How to load previously solved problems more quickly into my memory
  * Use a concrete example to wake up associated memory
  * Identify problem types and key points for that type of problems. e.g.
    * For stack type of problems, think about when to push/pop out of stack
    * For breath first search type of problems, think about starting point
    * For two-pointer type of problems, think about pointer start position(start/end position), increment/decrement pointer conditions
    * For binary search type of problems, think about whether to go left/right once mid is determined
    * For recursion type of problems, think about recursion base(arguments passed in), truning techniques, recursion order(child/parent first), recursion body, need backtracking
* Progressive enhancement on algorithms and data structures
  * algorithms
    * brute force first
    * trade space for time: e.g. hashmap in two-sum
    * pre-process data: e.g. sorting
    * divide into subproblems: e.g. recursion, discuss by different conditions
    * save time by avoid solving repeated problems: e.g. recursion -> dynamic programming
  * data structures
    * support lookup/delete by key: priorityqueue -> treemap
    * support enqueue/dequeue from both ends: queue -> deque
    * support insertion order on hashset/hashmap: hashset/hashmap -> linkedhashset/linkedhashmap
    * support larger character set for histogram problem: array -> map
  * algorithm time complexity for techniques: 
    * O(lgn): binary search
    * O(n): two pointers, use hashmap, partition
    * O(nlogn): priorityqueue, divide and conquer
    * O(n^2): dynamic programming
    * O(2^n): backtracking
    * O(n!): 
* Different strategies for different level of problems
	* for easy problems ( could complete 100% )
	  * fast, because might have follow-up questions
	  * focus more on communication / coding style / corner cases / exception handling
	* for medium problems
	  * try to be bug-free
	  * exhibit good coding habits
	    * write test cases before starting
	    * use comment placeholder to outline code before writing
	    * check code before finishing
	* for tricky/hard problems
	  * summarize an easy-to-remember pattern for each popular hard problem (e.g. regular expression matching, iterative post-order traversal)
	  * talk aloud so when stuck, interviewer could help

### Practice patterns <a id="practice-pattern"></a>
* **Tools - Task planning**: Use Eclipse task tags ( TO_START, TO_HURRY, TO_TEST ) to manage algorithm question status and prioritize important tasks
* **Feedbacks**: Use git commit number per day as feedback for progress
* **Summarizing lessons**: Use git commit message as a place to learn from mistakes and summarize lessons
* **Coding habit** - check code after finishing: Use JUnit to write and run test cases locally before going to online judge
* **Coding habit** - think about big picture before going to details: Never use debugger before thinking it through / walking it through by hands
* **Coding habit** - not just satisfied with running code but always pick the most elegant/efficient ways
* **Coding habit** - not just satisfied with fixing the bug but always think and generalize why the bug occurs
  
### Communication patterns <a id="communication-pattern"></a>
* Before writing the code
  1. declare interface in a strategic way (talk about different ways of defining it and trade-offs)
  2. clear assumptions about the problem, one type of assumption is about input validity; the other type is about input specifications (refer to "input-specifications" section)
  3. abstract the question
  4. come up with a brute force solution, calc time/space complexity
    * brain storm problem types (min/max, shortest distance, output solutions, search, topo sort), algorithms (recursion, backtracking, sorting, breath/depth-first search, two pointers) / data types (stack, heap, undirected/directed graph, trie) which might help in this problem
    * if stuck in this step, write a small and general example, think about how I will do it manually
    * if still having problems, ask interviewer for help tips
  5. (optional) optimize - strike a balance between time and space complexity
    * optimize from the perspective of space complexity
      * lots of repetitive computation: recursion -> dynamic programming --(optional)--> 2D memorization array to 1D --(optional)--> bit manipulation
      * top K: priorityQueue --> bucket sorting/partition algorithm
    * optimize from the perspective of time complexity
      * require O(logn) complexity: complete search -> binary search
      * require O(n) complexity -> two pointers/use hashmap
      * require O(nlogn) complexity: divide and conquer/priorityQueue
  6. Confirm with interviewer "Whether I am on the right track?". If no, go back to 4.
  7. Write some test cases
  8. Walk through test cases ( think about the boundary logics which is needed to be handled inside code ) 
* writing the code
  1. check input validity (throw exception or return directly)
  2. use // comments to outline the next block of code
    * Talk out the comments aloud
    * Writing part could be finished after writing the code. Leave a placeholder // temporarily 
* after writing the code
  1. check the code by myself
     1. review the entire code, check whether there are unused variables, dead while loops, formatting issues, boundaries index overflow/underflow , ...
     2. review the problem description, check whether there are unhandled problem assumptions 
     3. use small test cases to test different logical branches of the code
  2. talk about sections which could be refactored/improved, but was done in a certain way in an interview setting
  3. tell interviewer I have finished the problem


### Questions to confirm about input <a id="input-specification"></a>
* array
	* is array sorted
	* whether array entries contains positive/negative entries
	* given two arrays, which one's size is bigger
	* whether could modify entries inside array
* linkedList
	* doubly or singly linkedlist
* search related problems
    * return boolean or specific result
	* whether duplicates exist inside array
* hashmap
	* histogram-related problem, character set
	* whether hashmap key should be case-sensitive	
* String parser related problems
    * whether the string contains space
    * how are tokens separated, using comma, slash or something else
* Binary search tree
    * whether there are duplicated values. If yes, how are they stored (left <= middle < right)

### Java collections internals <a id="java-collections"></a>
* deque/stack: linkedlist
* hashmap: chaining ( array + list )
  * compute array index based on **public int hashCode()** method
  * decide list index based on **public boolean equals()** method
* linkedhashmap: hashtable with a linkedlist
* treemap: red-black tree
* priorityqueue: 

### Code snippets to remember <a id="snippets"></a>
* convert char to int, does not need explicit conversion
```java
value = value * 10 +  s.charAt( currPos ) - '0' ; 
```

#### Java basic apis <a id="basic-apis"></a>

* set.add(elem) return false if set already contains the elem
* list.sublist(startIndex, endIndex) returns a sublist of List
* recursive algorithm time complexity
  * T(n) = 2T(n/2) + O(n) = nlog(n)
* ListIterator benefits:
  * iterating bidirectional
  * add/remove elements while iterating
* Iterators

#### Math <a id="math"></a>
* divide two integers ( useful names: dividend/numerator, divisor/denominator, quotient, residue )
	* handle boundary cases ( 0, Integer.MIN_VALUE )
		- return int quotient
		- return double quotient
	* record quotient symbol ( neg/pos )
	* convert dividend and divisor to positive
	* calculate integer part 
	* calculate fraction part 
		- quotient = ( residue * 10 ) / divisor
		- residue = ( residue * 10 ) % divisor
		- use hashmap to record residue and occuring positions to handle recurring
	* concatenate symbol, integer part, dot, fraction part (possibly with parentheses)
* mod
	* judge whether a value is even or odd
		- Use num % 2 != 0 rather than num % 2 == 1 because of negative number mod ( e.g. -5 % 2 == -1 )
		- To guarantee mod result is always positive, if knowing num range RANGE, could consider ( num + RANGE ) % RANGE 
* power of integer: Java does not provide a built-in function for Integer values
    * solution 1: It has a built-in function double Math.pow( double, double ). But the computation cost for double is much higher than int and the result needs to be downcasted.
    * solution 2: Use multiply instead when exponent is low. 
	* solution 3: When 2 is radix, use bit shifting
	* solution 4: Implement in-house pow for integers based on divide and conquer
```java
// convert int decimal to binary format
int decimalNum = RANDOM_VALUE;
int[] binaryRepr = new int[32]; // for simplicity, binary format as an array
for ( int i = 0; i < 32; i++ )
{
	binaryRepr[i] = ( decimalNum >> i ) & 1;
}

// convert int binary to decimal format
int[] binaryRepr = new int[32];
int decimalNum = 0;
for ( int i = 0; i < 32; i++ )
{
	decimalNum |= ( binaryRepr[i] << i );
}
```
#### Array <a id="array"></a>
* Print arrays in Java
```java
int[] array1D = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
int[][] array2D = { { 1, 2 }, {2, 5}, {3, 7} };
System.out.println( Arrays.toString( array1D ) );
System.out.println( Arrays.deepToString( array2D ));
```
* Generate coordinate hash for a position (x,y) by x * width + y;

#### String <a id="string"></a>
* StringTokenizer ( like an iterator, has built-in hasNext() and next() func ). Could be used instead of a global position pointer inside recursive function (e.g. tree serialization and deserialization)
```java
String str = "This is String , split by StringTokenizer, created by mkyong";
StringTokenizer st = new StringTokenizer( str, "," );
while (st.hasMoreElements()) 
{
	System.out.println(st.nextElement());
}
```

* String[] split( String regex )
```java
String string = "004-034556";
String[] parts = string.split("-");
String part1 = parts[0]; // 004
String part2 = parts[1]; // 034556
```

* Parsing integer from a string. When possible, use Java's built-in function Integer Integer.ValueOf(String) or int Integer.ParseInt(String) instead of doing it manually
#### LinkedList <a id="linkedlist"></a>

#### Sort <a id="sort"></a>
* Judge whether intervals overlap
```java
private boolean isOverlap( Interval o1, Interval o2 )
{
	return !( o1.start >= o2.end 
			|| o2.start >= o1.end );
}
```
* Arrays.sort( array, comparator ) and Collections.sort( collection, comparator ) method

#### Binary search <a id="binary-search"></a>
* universal templates - iterative/recursive version 
```java
public int binarySearchIterative( int[] array, int target)
{
	int start = 0;
	int end = array.length - 1;
	while ( start + 1 < end )
	{
		int mid = ( end - start ) / 2 + start; // write in this way to avoid overflowing from " end + start "
		if ( array[mid] < target )
		{
			start = mid; // instead of mid + 1 to generalize the algorithm well
		}
		else
		{
			end = mid;
		}
	}
	// take result from start/end/non-exist
	// sometimes need to compare target directly to array[end], array[start]
	// sometimes need to see where target falls e.g. [~, array[start]), [array[start], array[end]), [array[end], ~)
	if ( array[end] == target )
	{
		return end;
	}
	else if ( array[start] == target )
	{
		return start;
	}
	else
	{
		return -1;
	}
}

public int binarySearchRecursive( int[] array, int target, int start, int end )
{
	// truning
	if ( start > end )
	{
		return -1;
	}
	// base condition
	if ( start + 1 >= end )
	{
		if ( array[start] == target )
		{
			return start;
		}
		else if ( array[end] == target )
		{
			return end;
		}
		else
		{
			return -1;
		}
	}
	// recursion body
	int mid = ( end - start ) / 2 + start;
	if ( array[mid] < target )
	{
		return binarySearchRecursive( array, target, mid, end );
	}
	else
	{
		return binarySearchRecursive( array, target, start, mid );
	}
}
```

* convert a range of binary search problem into variants of essence form
	- find first element smaller than target
		- e.g. find minimum element in rotated sorted array ( target: array[array.length-1])
	- find last element smaller than target
		- e.g. search insertion position
* how to handle duplicates in binary search

#### Stack <a id="stack"></a>
* When popping elements from stack, always check if the stack is empty. Otherwise, there might be a EmptyStackException()
* Elegant way to implement binary tree preorder/inorder/postorder traversal iteratively
```java
class Pair
{
	TreeNode node;
	int type; // 0 for first time, 1 for second time
	public Pair( TreeNode node, int type )
	{
		this.node = node;
		this.type = type;
	}
}

/** 
 * @param order  0 preorder; 1 inorder; 2 postorder
*/
public void traverse( TreeNode root, int order ) 
{
	Stack<Pair> stack = new Stack<>();
	stack.push( new Pair( root, 0 ) );
	while ( !stack.isEmpty() )
	{
		Pair stackTop = stack.pop();
		if ( stackTop.node == null )
		{
			continue;
		}
		if ( stackTop.type == 1 )
		{
			System.out.println(stackTop.node.value);
			continue;
		}
		switch ( order )
		{
			case 0:
				stack.push( new Pair( stackTop.node.rigth, 0 ) );
				stack.push( new Pair( stackTop.node.left, 0 ) );
				stack.push( new Pair( stackTop.node, 1 ) );
				break;
			case 1:
				stack.push( new Pair( stackTop.node.rigth, 0 ) );
				stack.push( new Pair( stackTop.node.left, 0 ) );
				stack.push( new Pair( stackTop.node, 1 ) );
				break;
			case 2:
				stack.push( new Pair( stackTop.node.rigth, 0 ) );
				stack.push( new Pair( stackTop.node.left, 0 ) );
				stack.push( new Pair( stackTop.node, 1 ) );
				break;				
		}
	}
}
```

#### Queue/priorityqueue <a id="queue"></a>
* Lambda expression inside PriorityQueue elements comparison
```java
PriorityQueue<NumAndFreq> mostFreqPrioQueue = new PriorityQueue<>( ( o1, o2 ) -> ( o2.freq - o1.freq ) ); // decreasing order
PriorityQueue<NumAndFreq> mostFreqPrioQueue = new PriorityQueue<>( ( o1, o2 ) -> ( o1.freq - o2.freq ) ); // increasing order
```
* use breath-first search queue for shortest path 
```java
 int bfsLevel = 0;
Queue<Integer> bfsQueue = new LinkedList<>();
bfsQueue.add( i * width + j );
while ( !bfsQueue.isEmpty() )
{
	int levelSize = bfsQueue.size(); // the number of nodes in one level can be obtained from the size of queue
	for ( int t = 0; t < levelSize; t++ )
	{
		int head = bfsQueue.remove();
  		// ... other stuff
    }
	bfsLevel++;
}
``` 

* treemap supports all operations by priorityqueue itself. In addition, it supports lookup by key.

#### Hashtable <a id="hashtable"></a>
* frequency count with hashmap
```java
map.put( key, 1 + map.getOrDefault( key, 0 ) );
```
* put if not exist
```java
map.putIfAbsent( key, new ArrayList<>() );
```
* Use double as hashmap keys
#### Recursive functions <a id="recursive"></a>

* Result wrapper class or customized classes
	* Used a lot in PriorityQueue, Recurse(Tree) related problems
	* the resultwrapper class should be a private inner class, rather than relying on the default package level visibility rule
```java
public class Solution
{
	private class NumAndFreq
	{
		public final int num;
		public final int freq;
		public NumAndFreq( int num, int freq )
		{
			this.num = num;
			this.freq = freq;
		}
	}
}
```

* If the problem is a recursive problem. But public API does not satisfy the arguments needed by recursive algorithm, consider declare one by yourself. In the example below, declare a private recursive method cloneGraphRecurse(node, Map) for public API cloneGraph(node)
```java
	public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) 
	{
		\\ validate input arguments before passing into 
		if ( node == null )
		{
			return null;
		}
		return cloneGraphRecurse( node, new HashMap<Integer, UndirectedGraphNode>() );
	}
	private UndirectedGraphNode cloneGraphRecurse( UndirectedGraphNode node, Map<Integer, UndirectedGraphNode> labelToNodeMap )
	{
		\\...
	}
```

* Modify java function primitive parameters ( Java so heavy, missing pointers inside C++, -_- )
	* Example problem: deserialize tree from String input. Return value is occupied by something else ( in this case TreeNode), but still want to change int argument position
```java
public TreeNode changePos( int position, String input ) // problem

public TreeNode changePos( int[] position, String input ) // Solution1: declare a global instance variable as position
public TreeNode changePos( List<Integer> position, String input ) // Solution2: Use an array/collection/customized type to wrap the primitive number
public TreeNode changePos( Position position, String input )
```	

#### Enumeration <a id="enumeration"></a>
* remove duplicates inside result

#### Depth first search <a id="dfs"></a>

#### Breath first search < id="bfs"></a>
* Grid-based problem concise snippets

#### Graph <a id="graph"></a>
* Detect cycles inside directed graphs with dfs + visited set + discovered set.
	* If during dfs in directed graph, a node discovered but not visited is encountered, then the directed graph has a cycle
```java
	public boolean hasCycle( Graph graph )
	{
	    // topoSort with dfs for detecting cycles
    	Set<Integer> discovered = new HashSet<>();
    	Set<Integer> visited = new HashSet<>();
    	for ( Integer vertex : graph.keySet() )
    	{
    		if ( !visited.contains( vertex ) )
    		{
    			if ( topoSort( graph, vertex, discovered, visited ) )
    			{
    				return false;
    			}
    		}
    	}
    	return true;
	}
    /**
     * @return whether a cycle is detected
     */
    private boolean topoSort ( Map<Integer, Set<Integer>> graph, Integer startNode, Set<Integer> discovered, Set<Integer> visited )
    {
    	discovered.add( startNode );
    	for ( Integer neighbor : graph.get( startNode ) )
    	{
    		if ( !discovered.contains( neighbor ) )
    		{
    			if ( topoSort( graph, neighbor, discovered, visited ) )
    			{
    				return true;
    			}
    		}
    		else if ( discovered.contains( neighbor ) 
    				&& !visited.contains( neighbor ) )
    		{
    			return true;
    		}
    		else
    		{
    			// already visited, do nothing
    			;
    		}
    	}
    	visited.add( startNode );
    	return false;
    }
```

#### Trie <a id="trie"></a>
* applicable when optimize for a list of words as dictionary, avoid recomputation for the same string prefix ( e.g. word search II, airbnb k distance question )
* iterative implementation much more concise than recursive implementation.
```java
class TrieNode 
{
    private final static int CHARSET_SIZE = 26;
    public TrieNode[] children;
    public boolean isLeaf;
    public char val;
    
    // Initialize your data structure here.
    public TrieNode() 
    {
        children = new TrieNode[CHARSET_SIZE];
    }
    
    public TrieNode( char val )
    {
        this();
        this.val = val;
    }
}

public class TrieIterative
{
    private TrieNode root;

    public TrieIterative() 
    {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    public void insert(String word) 
    {
        TrieNode currNode = root;
        for ( int i = 0; i < word.length(); i++ )
        {
            int nextNodePos = (int)( word.charAt( i ) - 'a' );
            if ( currNode.children[nextNodePos] == null )
            {
                TrieNode node = new TrieNode( word.charAt( i ) );
                currNode.children[nextNodePos] = node;
            }
            currNode = currNode.children[nextNodePos];

            if ( i == word.length() - 1 )
            {
                currNode.isLeaf = true;
            }
        }
    }
    
    // Returns if the word is in the trie.
    public boolean search( String word )
    {
        TrieNode currNode = root;
        for ( int i = 0; i < word.length(); i++ )
        {
            int nextNodePos = (int)( word.charAt( i ) - 'a' );

            if ( currNode.children[nextNodePos] == null )
            {
                return false;
            }
            // prefix exists, but not word
            if ( i == word.length() - 1 
                && !currNode.children[nextNodePos].isLeaf )
            {
                return false;
            }                

            currNode = currNode.children[nextNodePos];
        }
        return true;
    }

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) 
    {
        TrieNode currNode = root;
        for ( int i = 0; i < prefix.length(); i++ )
        {
            int nextNodePos = (int)( prefix.charAt( i ) - 'a' );

            if ( currNode.children[nextNodePos] == null )
            {
                return false;
            }

            currNode = currNode.children[nextNodePos];
        }
        return true;        
    }    
}
```

#### Dynamic-programming <a id="dynamic-programming"></a>
* when allocate dynamic programming table size, allocate additional one row/col for generalization

### Error-prone cases <a id="error-prone"></a>
* detect cycle in undirected graph
    - pass in super node inside dfs recursive call
* increase/decrease position counter inside foreach loop
* java list remove interface. Two list.remove() interface ( list.remove(int index), list.remove( Object object ) )
	- List<Integer> input
	- list.remove(index) will always take precedence because it does not require type casting
* passed in a reference variable (e.g. TreeNode, LinkNode, GraphNode...), check null pointer case
* boundary case summary
  * 2D array problem
	- check whether array2D.length == 0 and array2D[0].length == 0
  * Use 1D array based dynamic programming
	- check the size when array.length == 0 or array.length == 1
  * reference as input, such as collection (List, Map, ...) or string s
    - check s == null || s.length() == 0
* When a variable's name is really really long such as matrix[qHead.xCoor][qHead.yCoor+1] and it needs to be used in multiple places, it is really easy to create typos
* When a recursive function contains a long list of arguments, need to double check to make sure the arguments are correct
* Ternary operator ?: priority is only higher than assignment. If it is used in combination with other operators, parentheses should be added.
* Parsing integer from string, what if integer could be negative


### Smells for refactoring and optimization <a id="bad-smells"></a>
* code length > 100
* too many if statement checking for boundary cases
* code do not generalize well. Only work for current problem. e.g. merge 2 sorted list -> merge k sorted List

### Java sins <a id="java-sins"></a>
* linkedhashset could not be iterated reversely
* hard to return tuple values
* only pass by values

### Leetcode sins <a id="leetcode-sins"></a>
* When problem occurs, too few stack trace
* No online debuggers
* No history track along time axis. Really bad synchronous workflow
* Assumptions about validity of input
* Unable to mark different stages in solving a problem ( e.g. thought-out, implemented, optimized, on-line judged, summarized )
* Cannot add enough comments along the code
* Never-ending, ever-increasing number of problems