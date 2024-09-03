📚 Basic Concepts
1. What is a Linked List?
A linked list is a linear data structure where each element (node) contains:
    • Value (val): The data or value of the node.
    • Next (next): A reference (or pointer) to the next node in the sequence.
Visualization:

[Node1] -> [Node2] -> [Node3] -> [None]
    • Node1 has a value and points to Node2.
    • Node2 has a value and points to Node3.
    • Node3 has a value and points to None (end of the list).
Definition in Python:
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

    • val: Holds the value of the node.
    • next: Points to the next node.
2. Why Merge Linked Lists?
Merging sorted linked lists is a common problem where you combine multiple lists into one sorted list. It helps in understanding how to handle multiple sorted sequences efficiently.
Example:
    • List 1: 1 -> 4 -> 5
    • List 2: 1 -> 3 -> 4
    • List 3: 2 -> 6
Merged List: 1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6

📋 Problem Statement
You are given k sorted linked lists. Your task is to merge all these lists into one sorted linked list.
Input:
    • lists: A list of k linked lists, where each list is sorted in ascending order.
Output:
    • A single sorted linked list that merges all the input lists.

🛠 Solution Approach
We’ll solve this problem using the following steps:
    1. Initialize: Check if the input list is empty.
    2. Merge Lists: Use a helper function to merge two sorted linked lists.
    3. Iterate and Merge: Continuously merge pairs of lists until only one list remains.
1. Merge Two Sorted Lists
Concept: To merge two sorted lists into one sorted list, compare the nodes from each list and attach the smaller node to the result list.
Code for Merging Two Lists:
```
def mergeTwoLists(l1, l2):
    dummy = ListNode()  # Create a dummy node to simplify the merge process
    tail = dummy  # This will be the end of our merged list
    
    while l1 and l2:
        if l1.val < l2.val:
            tail.next = l1  # Attach l1 to the merged list
            l1 = l1.next  # Move l1 to the next node
        else:
            tail.next = l2  # Attach l2 to the merged list
            l2 = l2.next  # Move l2 to the next node
        tail = tail.next  # Move the tail pointer to the end of the merged list
    
    # Attach the remaining part of the non-empty list (if any)
    tail.next = l1 or l2
    
    return dummy.next  # Return the merged list, skipping the dummy node
```
Explanation:
    • Dummy Node: Helps simplify list operations. It acts as a placeholder.
    • Tail Pointer: Points to the last node of the merged list. We update it as we add new nodes.
    • While Loop: Compares nodes from l1 and l2. The smaller node is attached to tail.next, and we move forward in that list.
    • Remaining Nodes: After exiting the loop, one list might still have nodes left. We attach these remaining nodes.
2. Merge K Sorted Lists
Concept: Use the above helper function to iteratively merge lists in pairs until only one sorted list remains.
Code for Merging K Lists:
```
class Solution:
    def mergeKLists(self, lists):
        if not lists or len(lists) == 0:
            return None
        
        while len(lists) > 1:
            merged_lists = []
            for i in range(0, len(lists), 2):
                l1 = lists[i]
                l2 = lists[i+1] if (i+1) < len(lists) else None
                merged_lists.append(self.mergeTwoLists(l1, l2))
            lists = merged_lists
        
        return lists[0]
    
    def mergeTwoLists(self, l1, l2):
        dummy = ListNode()
        tail = dummy
        
        while l1 and l2:
            if l1.val < l2.val:
                tail.next = l1
                l1 = l1.next
            else:
                tail.next = l2
                l2 = l2.next
            tail = tail.next
        
        tail.next = l1 or l2
        
        return dummy.next
```




Explanation:
    • Initialization: Checks if the list of linked lists is empty.
    • While Loop: Merges lists in pairs. If the number of lists is odd, the last list is directly added to the merged lists.
    • Merge Function: Uses mergeTwoLists to combine pairs of lists.
    • Return: The final merged list.

🔧 Advanced Insights:
    • Time Complexity: The merging process has a time complexity of O(N log k), where N is the total number of nodes and k is the number of lists.
    • Space Complexity: The space complexity is O(1) if we exclude the space used by the output list.

I hope this detailed breakdown helps you understand the
