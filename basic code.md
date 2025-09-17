

## Table of Contents

1. Reverse a String (`ReverseString.java`)
2. Random 3-digit Number (`RandomThreeDigit.java`)
3. Detect Loop in Linked List (`DetectLoop.java`)
4. Set & Clear K-th Bit (`BitSetClear.java`)
5. Factorial (Recursion) (`FactorialRecursion.java`)
6. Stack using Linked List (`StackLinkedList.java`)

**Strings (5)**
7\. Palindrome Check (`StringPalindrome.java`)
8\. Count Vowels & Consonants (`CountVowelsConsonants.java`)
9\. First Non-Repeated Character (`FirstNonRepeatedChar.java`)
10\. Anagram Check (`AnagramCheck.java`)
11\. String Permutations (`StringPermutations.java`)

**Arrays (5)**
12\. Find Min & Max (`FindMinMax.java`)
13\. Reverse Array In-Place (`ReverseArrayInPlace.java`)
14\. Second Largest Element (`SecondLargest.java`)
15\. Check If Array Sorted (`IsArraySorted.java`)
16\. Remove Duplicates from Sorted Array (`RemoveDuplicatesSorted.java`)

**Linked List (5)**
17\. Reverse Linked List (`ReverseLinkedList.java`)
18\. Find Middle of Linked List (`MiddleOfLinkedList.java`)
19\. Detect and Remove Loop (`DetectAndRemoveLoop.java`)
20\. Merge Two Sorted Linked Lists (`MergeSortedLists.java`)
21\. Check if Linked List is Palindrome (`LinkedListPalindrome.java`)

**Bit Manipulation (5)**
22\. Check Power of Two (`IsPowerOfTwo.java`)
23\. Count Set Bits (`CountSetBits.java`)
24\. Swap Two Numbers Without Temp (`SwapWithoutTemp.java`)
25\. Find Unique Element (others appear twice) (`SingleNonRepeating.java`)
26\. Toggle K-th Bit (`ToggleKthBit.java`)

**Recursion (5)**
27\. Fibonacci (Recursion) (`FibonacciRecursion.java`)
28\. Sum of Digits (Recursion) (`SumOfDigits.java`)
29\. Tower of Hanoi (`TowerOfHanoi.java`)
30\. Reverse Number (Recursion) (`ReverseNumberRecursion.java`)
31\. Generate All Subsets (Recursion/backtracking) (`GenerateSubsets.java`)

---

> Below each entry you’ll find:
>
> * Brief description & approach
> * Complexity (Time, Space)
> * Full Java code (self-contained `main`)
> * Sample input/output (in comments or `main`)

---

## 1. Reverse a String — `ReverseString.java`

**Description:** Reverse a string using in-place character swap (two-pointer).
**Approach:** Convert to `char[]`, swap `i` and `n-1-i` until midpoint.
**Time:** O(n) — one pass.
**Space:** O(n) for char array (can be considered O(1) extra).

```java
// ReverseString.java
public class ReverseString {
    public static String reverse(String s) {
        if (s == null) return null;
        char[] a = s.toCharArray();
        int i = 0, j = a.length - 1;
        while (i < j) {
            char tmp = a[i];
            a[i++] = a[j];
            a[j--] = tmp;
        }
        return new String(a);
    }

    public static void main(String[] args) {
        String input = "Visteon";
        System.out.println("Original: " + input);
        System.out.println("Reversed: " + reverse(input)); // Reversed: noetsiV
    }
}
```

---

## 2. Generate Random 3-Digit Number — `RandomThreeDigit.java`

**Description:** Generate a number between 100 and 999 inclusive.
**Approach:** Use `Random.nextInt(900)` and add 100.
**Time:** O(1), **Space:** O(1).

```java
// RandomThreeDigit.java
import java.util.Random;

public class RandomThreeDigit {
    public static int random3Digit() {
        Random rand = new Random();
        return 100 + rand.nextInt(900); // 0..899 -> 100..999
    }

    public static void main(String[] args) {
        System.out.println("Random 3-digit: " + random3Digit());
    }
}
```

---

## 3. Detect Loop in Linked List (Floyd’s) — `DetectLoop.java`

**Description:** Use Floyd’s cycle-finding algorithm (slow/fast pointers).
**Approach:** Move `slow` by 1 and `fast` by 2; if they meet → loop.
**Time:** O(n), **Space:** O(1).

```java
// DetectLoop.java
public class DetectLoop {
    static class Node {
        int val;
        Node next;
        Node(int v) { val = v; }
    }

    public static boolean hasLoop(Node head) {
        Node slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) return true;
        }
        return false;
    }

    public static void main(String[] args) {
        Node head = new Node(1);
        head.next = new Node(2);
        head.next.next = new Node(3);
        head.next.next.next = head.next; // loop at node with val=2
        System.out.println("Has loop: " + hasLoop(head)); // true
    }
}
```

---

## 4. Set & Clear K-th Bit — `BitSetClear.java`

**Description:** Show how to set and clear the k-th bit (1-indexed k).
**Approach:** `set: n | (1 << (k-1))`, `clear: n & ~(1 << (k-1))`.
**Time:** O(1), **Space:** O(1).

```java
// BitSetClear.java
public class BitSetClear {
    static int setKth(int n, int k) {
        return n | (1 << (k - 1));
    }
    static int clearKth(int n, int k) {
        return n & ~(1 << (k - 1));
    }

    public static void main(String[] args) {
        int n = 5; // 0101
        int k = 2;
        System.out.println("Original: " + n);
        System.out.println("Set " + k + "th bit: " + setKth(n, k));   // 7 (0111)
        System.out.println("Clear " + k + "th bit: " + clearKth(n, k)); // 5 & ~2 = 5 & (~0010) = 0101 & 1101 = 0101 -> 5
    }
}
```

---

## 5. Factorial (Recursion) — `FactorialRecursion.java`

**Description:** Compute factorial using recursion. Show base case to avoid infinite recursion.
**Time:** O(n), **Space:** O(n) recursion stack.

```java
// FactorialRecursion.java
public class FactorialRecursion {
    static long factorial(int n) {
        if (n <= 1) return 1L;
        return n * factorial(n - 1);
    }

    public static void main(String[] args) {
        int n = 10;
        System.out.printf("Factorial of %d = %d\n", n, factorial(n)); // 3628800
    }
}
```

---

## 6. Stack Implementation using Linked List — `StackLinkedList.java`

**Description:** Linked-list-based stack with push/pop/peek/display.
**Time:** push/pop O(1), **Space:** O(n).

```java
// StackLinkedList.java
public class StackLinkedList {
    static class Node {
        int val;
        Node next;
        Node(int v) { val = v; }
    }

    static class Stack {
        private Node top;
        public void push(int x) {
            Node node = new Node(x);
            node.next = top;
            top = node;
        }
        public Integer pop() {
            if (top == null) return null;
            int v = top.val;
            top = top.next;
            return v;
        }
        public Integer peek() {
            return top == null ? null : top.val;
        }
        public void display() {
            Node cur = top;
            System.out.print("Stack top -> ");
            while (cur != null) {
                System.out.print(cur.val + " ");
                cur = cur.next;
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        Stack s = new Stack();
        s.push(10); s.push(20); s.push(30);
        s.display(); // top-> 30 20 10
        System.out.println("Popped: " + s.pop()); // 30
        s.display();
    }
}
```

---

# Strings — 5 Programs

## 7. Palindrome Check (ignore non-alphanumeric & case) — `StringPalindrome.java`

**Approach:** Two-pointer, skip non-alphanumeric, compare lowercased chars.
**Time:** O(n), **Space:** O(1).

```java
// StringPalindrome.java
public class StringPalindrome {
    public static boolean isPalindrome(String s) {
        if (s == null) return false;
        int i = 0, j = s.length() - 1;
        while (i < j) {
            while (i < j && !Character.isLetterOrDigit(s.charAt(i))) i++;
            while (i < j && !Character.isLetterOrDigit(s.charAt(j))) j--;
            if (Character.toLowerCase(s.charAt(i)) != Character.toLowerCase(s.charAt(j))) return false;
            i++; j--;
        }
        return true;
    }

    public static void main(String[] args) {
        System.out.println(isPalindrome("A man, a plan, a canal: Panama")); // true
        System.out.println(isPalindrome("race a car")); // false
    }
}
```

---

## 8. Count Vowels & Consonants — `CountVowelsConsonants.java`

**Approach:** Iterate characters, check `Character.isLetter`, then check vowels set.
**Time:** O(n), **Space:** O(1).

```java
// CountVowelsConsonants.java
public class CountVowelsConsonants {
    public static void count(String s) {
        int vowels = 0, consonants = 0;
        for (char c : s.toCharArray()) {
            if (Character.isLetter(c)) {
                char lc = Character.toLowerCase(c);
                if ("aeiou".indexOf(lc) >= 0) vowels++;
                else consonants++;
            }
        }
        System.out.printf("Vowels: %d, Consonants: %d\n", vowels, consonants);
    }

    public static void main(String[] args) {
        count("Hello World!"); // Vowels: 3, Consonants: 7
    }
}
```

---

## 9. First Non-Repeated Character — `FirstNonRepeatedChar.java`

**Approach:** Use `LinkedHashMap` to count and preserve order.
**Time:** O(n), **Space:** O(1) limited by charset or O(n) worst.

```java
// FirstNonRepeatedChar.java
import java.util.LinkedHashMap;
import java.util.Map;

public class FirstNonRepeatedChar {
    public static Character firstNonRepeated(String s) {
        if (s == null) return null;
        LinkedHashMap<Character, Integer> count = new LinkedHashMap<>();
        for (char c : s.toCharArray()) count.put(c, count.getOrDefault(c, 0) + 1);
        for (Map.Entry<Character, Integer> e : count.entrySet()) {
            if (e.getValue() == 1) return e.getKey();
        }
        return null;
    }

    public static void main(String[] args) {
        System.out.println(firstNonRepeated("swiss")); // w
        System.out.println(firstNonRepeated("aabb")); // null
    }
}
```

---

## 10. Anagram Check — `AnagramCheck.java`

**Approach:** Normalize (remove spaces, lowercase), sort chars and compare or use frequency array. We’ll sort (simple & general).
**Time:** O(n log n), **Space:** O(n).

```java
// AnagramCheck.java
import java.util.Arrays;

public class AnagramCheck {
    public static boolean areAnagrams(String a, String b) {
        if (a == null || b == null) return false;
        String sa = a.replaceAll("\\s+", "").toLowerCase();
        String sb = b.replaceAll("\\s+", "").toLowerCase();
        if (sa.length() != sb.length()) return false;
        char[] A = sa.toCharArray();
        char[] B = sb.toCharArray();
        Arrays.sort(A); Arrays.sort(B);
        return Arrays.equals(A, B);
    }

    public static void main(String[] args) {
        System.out.println(areAnagrams("listen", "silent")); // true
        System.out.println(areAnagrams("hello", "bello")); // false
    }
}
```

---

## 11. String Permutations (recursion in-place) — `StringPermutations.java`

**Approach:** Swap characters recursively. For duplicates, you could filter but simple version prints all permutations.
**Time:** O(n \* n!), **Space:** O(n) recursion.

```java
// StringPermutations.java
public class StringPermutations {
    static void permute(char[] a, int l) {
        if (l == a.length - 1) {
            System.out.println(new String(a));
            return;
        }
        for (int i = l; i < a.length; i++) {
            swap(a, l, i);
            permute(a, l + 1);
            swap(a, l, i); // backtrack
        }
    }
    static void swap(char[] a, int i, int j) {
        char tmp = a[i]; a[i] = a[j]; a[j] = tmp;
    }

    public static void main(String[] args) {
        String s = "ABC";
        permute(s.toCharArray(), 0);
        // Output: ABC ACB BAC BCA CBA CAB
    }
}
```

---

# Arrays — 5 Programs

## 12. Find Minimum & Maximum in Array — `FindMinMax.java`

**Approach:** Single pass scan; initialize with first element.
**Time:** O(n), **Space:** O(1).

```java
// FindMinMax.java
public class FindMinMax {
    public static void find(int[] arr) {
        if (arr == null || arr.length == 0) {
            System.out.println("Empty array");
            return;
        }
        int min = arr[0], max = arr[0];
        for (int v : arr) {
            if (v < min) min = v;
            if (v > max) max = v;
        }
        System.out.printf("Min: %d, Max: %d\n", min, max);
    }

    public static void main(String[] args) {
        find(new int[] {3, 1, 4, 1, 5, 9});
    }
}
```

---

## 13. Reverse Array In-Place — `ReverseArrayInPlace.java`

**Approach:** two-pointer swap.
**Time:** O(n), **Space:** O(1).

```java
// ReverseArrayInPlace.java
import java.util.Arrays;

public class ReverseArrayInPlace {
    public static void reverse(int[] arr) {
        if (arr == null) return;
        int i = 0, j = arr.length - 1;
        while (i < j) {
            int tmp = arr[i]; arr[i++] = arr[j]; arr[j--] = tmp;
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        reverse(arr);
        System.out.println(Arrays.toString(arr)); // [5, 4, 3, 2, 1]
    }
}
```

---

## 14. Second Largest Element — `SecondLargest.java`

**Approach:** Track `max` and `secondMax`. Handle duplicates and arrays with fewer than 2 distinct numbers.
**Time:** O(n), **Space:** O(1).

```java
// SecondLargest.java
public class SecondLargest {
    public static Integer secondLargest(int[] arr) {
        if (arr == null) return null;
        Integer max = null, second = null;
        for (int v : arr) {
            if (max == null || v > max) {
                second = max;
                max = v;
            } else if ((second == null || v > second) && v != max) {
                second = v;
            }
        }
        return second;
    }

    public static void main(String[] args) {
        System.out.println(secondLargest(new int[] {5, 1, 5, 4, 3})); // 4
        System.out.println(secondLargest(new int[] {1, 1, 1})); // null (no second distinct)
    }
}
```

---

## 15. Check If Array is Sorted (non-decreasing) — `IsArraySorted.java`

**Approach:** One-pass compare arr\[i] <= arr\[i+1].
**Time:** O(n), **Space:** O(1).

```java
// IsArraySorted.java
public class IsArraySorted {
    public static boolean isSorted(int[] arr) {
        if (arr == null || arr.length <= 1) return true;
        for (int i = 0; i < arr.length - 1; i++) {
            if (arr[i] > arr[i + 1]) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        System.out.println(isSorted(new int[] {1,2,2,3})); // true
        System.out.println(isSorted(new int[] {3,2,1})); // false
    }
}
```

---

## 16. Remove Duplicates from Sorted Array — `RemoveDuplicatesSorted.java`

**Approach:** Two-pointer, in-place; return new length.
**Time:** O(n), **Space:** O(1).

```java
// RemoveDuplicatesSorted.java
import java.util.Arrays;

public class RemoveDuplicatesSorted {
    public static int remove(int[] arr) {
        if (arr == null) return 0;
        if (arr.length <= 1) return arr.length;
        int j = 0;
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] != arr[j]) arr[++j] = arr[i];
        }
        return j + 1;
    }

    public static void main(String[] args) {
        int[] arr = {1,1,2,2,3,3,4};
        int len = remove(arr);
        System.out.println("New length: " + len + ", Array: " + Arrays.toString(Arrays.copyOf(arr, len)));
        // New length: 4, Array: [1, 2, 3, 4]
    }
}
```

---

# Linked List — 5 Programs

> We'll use a simple `Node` class in each file for readability and independence.

## 17. Reverse Linked List (iterative) — `ReverseLinkedList.java`

**Approach:** Iteratively reverse using `prev`, `cur`, `next`.
**Time:** O(n), **Space:** O(1).

```java
// ReverseLinkedList.java
public class ReverseLinkedList {
    static class Node { int val; Node next; Node(int v) { val=v; } }
    static Node reverse(Node head) {
        Node prev = null, cur = head;
        while (cur != null) {
            Node next = cur.next;
            cur.next = prev;
            prev = cur;
            cur = next;
        }
        return prev;
    }

    public static void main(String[] args) {
        Node a = new Node(1);
        a.next = new Node(2); a.next.next = new Node(3);
        Node r = reverse(a);
        while (r != null) { System.out.print(r.val + " "); r = r.next; } // 3 2 1
    }
}
```

---

## 18. Find Middle of Linked List — `MiddleOfLinkedList.java`

**Approach:** Slow-fast pointers; slow will be middle when fast reaches end.
**Time:** O(n), **Space:** O(1).

```java
// MiddleOfLinkedList.java
public class MiddleOfLinkedList {
    static class Node { int val; Node next; Node(int v) { val=v; } }
    static Node middle(Node head) {
        if (head == null) return null;
        Node slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    public static void main(String[] args) {
        Node a = new Node(1); a.next = new Node(2); a.next.next = new Node(3); a.next.next.next = new Node(4);
        Node mid = middle(a);
        System.out.println("Middle: " + mid.val); // 3 for even-length returns second middle (3)
    }
}
```

---

## 19. Detect and Remove Loop — `DetectAndRemoveLoop.java`

**Approach:** Use Floyd to detect, then reset one pointer to head and move both until next pointers match; break loop.
**Time:** O(n), **Space:** O(1).

```java
// DetectAndRemoveLoop.java
public class DetectAndRemoveLoop {
    static class Node { int val; Node next; Node(int v) { val=v; } }

    static boolean detectAndRemove(Node head) {
        Node slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next; fast = fast.next.next;
            if (slow == fast) { removeLoop(head, slow); return true; }
        }
        return false;
    }

    static void removeLoop(Node head, Node meeting) {
        Node ptr1 = head;
        Node ptr2 = meeting;
        // If loop starts at head, special-case: find last node
        if (ptr2 == head) {
            while (ptr2.next != head) ptr2 = ptr2.next;
            ptr2.next = null;
            return;
        }
        while (ptr1.next != ptr2.next) {
            ptr1 = ptr1.next;
            ptr2 = ptr2.next;
        }
        ptr2.next = null;
    }

    public static void main(String[] args) {
        Node head = new Node(1);
        head.next = new Node(2); head.next.next = new Node(3); head.next.next.next = new Node(4);
        head.next.next.next.next = head.next; // loop at node 2
        System.out.println("Loop existed: " + detectAndRemove(head)); // true
        // print list after removal
        Node cur = head;
        while (cur != null) { System.out.print(cur.val + " "); cur = cur.next; } // 1 2 3 4
    }
}
```

---

## 20. Merge Two Sorted Linked Lists — `MergeSortedLists.java`

**Approach:** Iterative merge using dummy head.
**Time:** O(n+m), **Space:** O(1).

```java
// MergeSortedLists.java
public class MergeSortedLists {
    static class Node { int val; Node next; Node(int v) { val=v; } }

    static Node merge(Node a, Node b) {
        Node dummy = new Node(0), tail = dummy;
        while (a != null && b != null) {
            if (a.val <= b.val) { tail.next = a; a = a.next; }
            else { tail.next = b; b = b.next; }
            tail = tail.next;
        }
        tail.next = (a != null) ? a : b;
        return dummy.next;
    }

    public static void main(String[] args) {
        Node a = new Node(1); a.next = new Node(3); a.next.next = new Node(5);
        Node b = new Node(2); b.next = new Node(4); b.next.next = new Node(6);
        Node m = merge(a, b);
        while (m != null) { System.out.print(m.val + " "); m = m.next; } // 1 2 3 4 5 6
    }
}
```

---

## 21. Check if Linked List is Palindrome — `LinkedListPalindrome.java`

**Approach:** Find middle, reverse second half, compare halves, optionally restore list.
**Time:** O(n), **Space:** O(1).

```java
// LinkedListPalindrome.java
public class LinkedListPalindrome {
    static class Node { int val; Node next; Node(int v) { val=v; } }

    static boolean isPalindrome(Node head) {
        if (head == null || head.next == null) return true;
        // find middle
        Node slow = head, fast = head;
        while (fast != null && fast.next != null) { slow = slow.next; fast = fast.next.next; }
        // reverse second half
        Node second = reverse(slow);
        Node first = head;
        Node tmpSecond = second;
        boolean pal = true;
        while (tmpSecond != null) {
            if (first.val != tmpSecond.val) { pal = false; break; }
            first = first.next; tmpSecond = tmpSecond.next;
        }
        reverse(second); // restore (optional)
        return pal;
    }

    static Node reverse(Node head) {
        Node prev = null, cur = head;
        while (cur != null) { Node nxt = cur.next; cur.next = prev; prev = cur; cur = nxt; }
        return prev;
    }

    public static void main(String[] args) {
        Node h = new Node(1); h.next = new Node(2); h.next.next = new Node(2); h.next.next.next = new Node(1);
        System.out.println("Is palindrome: " + isPalindrome(h)); // true
    }
}
```

---

# Bit Manipulation — 5 Programs

## 22. Check Power of Two — `IsPowerOfTwo.java`

**Approach:** `n > 0 && (n & (n-1)) == 0`.
**Time:** O(1), **Space:** O(1).

```java
// IsPowerOfTwo.java
public class IsPowerOfTwo {
    public static boolean isPowerOfTwo(int n) {
        return n > 0 && (n & (n - 1)) == 0;
    }

    public static void main(String[] args) {
        System.out.println(isPowerOfTwo(16)); // true
        System.out.println(isPowerOfTwo(18)); // false
    }
}
```

---

## 23. Count Set Bits — `CountSetBits.java`

**Approach:** Brian Kernighan’s algorithm: repeatedly `n &= (n-1)` until zero.
**Time:** O(number\_of\_set\_bits), worst O(32), **Space:** O(1).

```java
// CountSetBits.java
public class CountSetBits {
    public static int countSetBits(int n) {
        int count = 0;
        while (n != 0) {
            count++;
            n &= (n - 1);
        }
        return count;
    }

    public static void main(String[] args) {
        System.out.println(countSetBits(13)); // 3 (1101)
    }
}
```

---

## 24. Swap Two Numbers Without Third Variable — `SwapWithoutTemp.java`

**Approach:** XOR-based swap: `a = a ^ b; b = a ^ b; a = a ^ b;` (works for integers). Be careful if `a == b` — result becomes 0 (but XOR swap actually works fine with same values — it results in original values; still safe). You can also use addition/subtraction but risk overflow. We'll show XOR.
**Time:** O(1), **Space:** O(1).

```java
// SwapWithoutTemp.java
public class SwapWithoutTemp {
    public static void swapXor() {
        int a = 10, b = 20;
        System.out.println("Before: a=" + a + ", b=" + b);
        a = a ^ b;
        b = a ^ b;
        a = a ^ b;
        System.out.println("After: a=" + a + ", b=" + b);
    }

    public static void main(String[] args) { swapXor(); }
}
```

---

## 25. Find Only Non-Repeating Element (others repeat twice) — `SingleNonRepeating.java`

**Approach:** XOR all elements; duplicates cancel out.
**Time:** O(n), **Space:** O(1).

```java
// SingleNonRepeating.java
public class SingleNonRepeating {
    public static int findSingle(int[] arr) {
        int res = 0;
        for (int v : arr) res ^= v;
        return res;
    }

    public static void main(String[] args) {
        int[] arr = {2, 3, 5, 4, 5, 3, 4};
        System.out.println(findSingle(arr)); // 2
    }
}
```

---

## 26. Toggle K-th Bit — `ToggleKthBit.java`

**Approach:** XOR with mask `1 << (k - 1)`.
**Time:** O(1), **Space:** O(1).

```java
// ToggleKthBit.java
public class ToggleKthBit {
    public static int toggle(int n, int k) {
        return n ^ (1 << (k - 1));
    }

    public static void main(String[] args) {
        int n = 5; // 0101
        int k = 1;
        System.out.println(toggle(n, k)); // toggles least significant bit: 0101 ^ 0001 = 0100 -> 4
    }
}
```

---

# Recursion — 5 Programs

## 27. Fibonacci (naive recursion) — `FibonacciRecursion.java`

**Approach:** `fib(n) = fib(n-1) + fib(n-2)` with base cases. (Naive exponential time; for interviews mention DP/memoization.)
**Time:** O(φ^n) (exponential), **Space:** O(n) recursion.

```java
// FibonacciRecursion.java
public class FibonacciRecursion {
    public static int fib(int n) {
        if (n <= 1) return n;
        return fib(n - 1) + fib(n - 2);
    }

    public static void main(String[] args) {
        System.out.println(fib(10)); // 55
    }
}
```

---

## 28. Sum of Digits (recursion) — `SumOfDigits.java`

**Approach:** `sum(n) = n%10 + sum(n/10)` base `n==0`.
**Time:** O(digits), **Space:** O(digits).

```java
// SumOfDigits.java
public class SumOfDigits {
    public static int sumDigits(int n) {
        n = Math.abs(n);
        if (n == 0) return 0;
        return n % 10 + sumDigits(n / 10);
    }

    public static void main(String[] args) {
        System.out.println(sumDigits(12345)); // 15
    }
}
```

---

## 29. Tower of Hanoi — `TowerOfHanoi.java`

**Approach:** Classic recursion: move `n-1` from src to aux, move disk n to dest, move `n-1` aux to dest.
**Time:** O(2^n), **Space:** O(n).

```java
// TowerOfHanoi.java
public class TowerOfHanoi {
    static void move(int n, char from, char to, char aux) {
        if (n == 1) {
            System.out.printf("Move disk 1 from %c to %c\n", from, to);
            return;
        }
        move(n - 1, from, aux, to);
        System.out.printf("Move disk %d from %c to %c\n", n, from, to);
        move(n - 1, aux, to, from);
    }

    public static void main(String[] args) {
        move(3, 'A', 'C', 'B');
    }
}
```

---

## 30. Reverse Number using Recursion (tail recursion) — `ReverseNumberRecursion.java`

**Approach:** Use helper that carries reversed number as accumulator: `helper(n, rev)`.
**Time:** O(digits), **Space:** O(digits).

```java
// ReverseNumberRecursion.java
public class ReverseNumberRecursion {
    public static long reverseNumber(long n) {
        return helper(Math.abs(n), 0);
    }

    private static long helper(long n, long rev) {
        if (n == 0) return rev;
        return helper(n / 10, rev * 10 + (n % 10));
    }

    public static void main(String[] args) {
        System.out.println(reverseNumber(12345)); // 54321
    }
}
```

---

## 31. Generate All Subsets (Power Set) — `GenerateSubsets.java`

**Approach:** Backtracking recursion: for each element choose include/exclude.
**Time:** O(n \* 2^n) to generate and print all subsets, **Space:** O(n) recursion.

```java
// GenerateSubsets.java
import java.util.ArrayList;
import java.util.List;

public class GenerateSubsets {
    static void subsets(int[] arr) {
        List<Integer> current = new ArrayList<>();
        backtrack(arr, 0, current);
    }

    static void backtrack(int[] arr, int idx, List<Integer> cur) {
        if (idx == arr.length) {
            System.out.println(cur);
            return;
        }
        // Exclude arr[idx]
        backtrack(arr, idx + 1, cur);
        // Include arr[idx]
        cur.add(arr[idx]);
        backtrack(arr, idx + 1, cur);
        cur.remove(cur.size() - 1);
    }

    public static void main(String[] args) {
        subsets(new int[] {1, 2, 3});
        // Output: [] [3] [2] [2, 3] [1] [1, 3] [1, 2] [1, 2, 3] (order may vary due to recursion order)
    }
}
```

---

# Notes, Tips & Edge Cases

* **String permutations** explode quickly — only use for small strings (<= 8 typically).
* **Factorial** and **Fibonacci (naive)** are not safe for large `n` due to overflow / exponential runtime. Mention DP / iterative solutions when asked.
* For **bit manipulation** be careful about signed integers; Java uses 32-bit signed ints. If working with very large bit patterns, consider `long` (64-bit).
* For linked list code, each file has its own `Node` class for clarity. In a real project you would reuse one `Node` class.
* **Loop detection removal**: special-case when loop includes head (addressed in code).
* **Swap using XOR**: works for primitives. Avoid when swapping same variable reference intentionally; safer to use temp in production code.

---
