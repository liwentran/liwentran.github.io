# Linked List
A linked list is a linear data structure in which the elements, called *nodes* are not stored at contiguous memory locations (in contrast to arrays). 
Each *node* comprises of two items- the data it stores and a pointer to the next node. 
- Last node's next pointer points to `NULL`
- In an empty linked list, the *head pointer* points to `NULL`.

![](Pasted%20image%2020211010175207.png)

A pointer called "head" will store the address of the first node of the linked list. 

## Linked List vs Array

| Array	| Linked List |
|---|---|
| size of the array is fixed | sized of linked list is not fixed|
| occupies less memory for the same number of elements | requires more space because of "next" |
| accessing i'th value is fast using indicies (simple arithmetic) | has to traverse the list from start |
| inserting new elements is expensive | after deciding where to add, is straightforward (no shifting) |
| no deleting without shifting items | deleting is easy (kind of) |

## Implementation
You can define node as a new struct. It will consist of a variable of the data type of the data and a pointer to a `Node`. `create_node` creates one isolated node. 
```c
typedef struct _node {
	char data;	// could be any time
	struct _node * next; // self-referential
} Node;

Node * create_node (char ch) {
	Node * node = (Node *) malloc(sizeof(Node));
	node->data = ch;
	node->next = NULL; // one node by itself.
	return node;
}
```

## Linked List Operations
### print
*print* - output all data items in order from head to tail.
```c
void print(const Node * cur)
```
use a Node pointer named `cur` to advance node by node through the list and each time `cur` encounters another node, output that node's data value. 

### length
*length* - reports number of items currently in list
```c
long length(const Node * cur)
```
use a Node pointer named `cur` to advance node by node through list, and increment a counter each time `cur` encounters another node. 

### add_after
*add_after* - insert new node with a given data value immediately after a given existing node. 
```c
void add_after(Node * node, char val) 
```
`val` parameter is data value to place in new node. `node` parameter holds address of existing node that new one should be placed right after. 
New node needs to be dynamically allocated.
Additional statements are needed to adjust links appropriately so list stays connected. 

### clear
*clear* - deallocates all nodes in the list, sets head pointer to null. 

### add_front
*add_front* - creates a new node and makes it the first node of the list.
```c
void add_front(Node ** list_ptr, char val) {
	Node * = create_node(val);
	n->next = *list_ptr; // node's next gets address of old first node
	*list_ptr = n; // head pointer gets address of new node
}
```
The function needs the ability to modify the actual head pointer (not a copy), so call with `&head` as argument.

### clear_list
*clear_list* - free all nodes.

### remove_after
*remove_after* - remove the node that is after the given node. 
```c
char delete_after (Node * node);
```
![](linked%20list%20remove_after().png)

### remove_front
*remove_front* - remove the first node and makes the second node the first node. 
```c
char delete_front(Node **list_ptr);
```
![](linkedl%20list%20remove_front().png)

### remove_all
*remove_all* - remove all occurences of a particular data value. 

### More about Head
Some of these operations require modification of the head. Head is on the stack (while the nodes are on the heap), so when we call the functions that modify the head, we need to make sure we pass the address of head (pass the pointer of the pointer). 
- Note: pointers are pass by values, so changes to p will NOT affect p. 
- If the function needs to update head, then that function should accept a double pointer. 
	- Address of the first node = `*list_ptr*` 