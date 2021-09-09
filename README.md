# Days 1-2: Implement a Linked List

## Learning Goals

- Define the characteristics of a linked list
- Implement a common methods of a linked list class

## Introduction

In this lesson, we'll be implementing a **linked list** data structure. More
specifically, we'll be implementing a singly-linked list, or simple linked list
(it goes by several names). A **linked list** consists of **nodes**, which are
connected to one another. It is similar to an array in that its elements (nodes)
are in a specific order.

![Linked List](https://curriculum-content.s3.amazonaws.com/data-structures-and-algorithms/what-is-a-linked-list/linked_list.png)

We may choose to use linked lists in place of other data structures when we need
fast insertion and deletion of data.

The node at the beginning of the list is called the `head`, while the node at
the end is called the `tail`.

## What Is a Node?

A **node** in a linked list is an object that has two attributes: `value` and
`next`. The `value` stores the data that we might be interested in retrieving,
such as an integer, array, string, or some other object. The `next` attribute
points to the next node in the list.

```txt
array = [1, 2]
head = new Node(value: 1)
nextNode = new Node(value: 2)
head.next = nextNode
// head -> nextNode
```

The very last node in the linked list will point to nothing, so its `next` value
may be `undefined`, `null`, `nil`, etc. It depends on the language being used
and on the implementation of the node class.

## How Do We Track the Starting Node of a Linked List?

It is common to define a class called `LinkedList` when using this data
structure. The `LinkedList` class stores the `head` node, which points to the
start of the list. As long as we know where the list starts, we can always
traverse it to access all other nodes in the list by using the `next` property.

```txt
head = new Node(value: 'i am the beginning!')
list = new LinkedList(head)
```

> A note on online algorithm challenges: When completing challenges online, such
> as through LeetCode, you might be provided with only the head node, rather
> than a `LinkedList` class.

## How Do We Visit Each Node?

Iterables, like arrays, provide instance methods that allow us to traverse them,
and we can also traverse them using loops and indices. Linked lists are a little
different. Nodes do not have indexes: they just point to the next node, or to
nothing if it's the last node in the list (the `tail`). This means we have to go
to the `head` node, ask it what's next, go there, and repeat!

Here's an example using people waiting in a queue to get into a club to dance to
some sick beats! In order, the queue consists of Janzz, Murray, and Lakshmi.

```txt
You: "Hey Janzz! Who's next?"
Janzz: "Murray"
You: "Hey Murray! Who's next?"
Murray: "Lakshmi"
You: "Hey Lakshmi! Who's next?"
Lakshmi: [awkward silence]
```

We're not giving you the code here because we want you to figure out how to
traverse a linked list for yourself later on. We believe in you!

## Summary

A **linked list** is a data structure consisting of **nodes**. The `head` node
denotes the start of the list.

Each node has two attributes: `value` and `next`. `value` stores the data we
might be interested in retrieving, while `next` points to the next Node in the
list. The last node, called the `tail`, in the list points to nothing (e.g.
`next` is `null`), and that's how we know it's the end!

We can use another class called `LinkedList` to track the `head` of the list.

## Implement a Linked List

Please note that in Ruby we'll be using `next_node` instead of `next` as the
`Node` attribute. This is to avoid confusing syntax, since next is a reserved
keyword in Ruby. It also leads to confusing syntax highlighting as a result. In
short, wherever you see `next`, think `next_node` for Ruby.

Use the language of your choosing. We've included starter files for some
languages where you can pseudocode, and optionally explain your solution and
code.

### 1. Define the `Node` Class

A `Node` has two attributes: `value` and `next`. `value` can store anything,
while `next` will either point to the next `Node` or to nothing.

Provide default values for both `value` and `next` so that a new Node can be
instantiated without any arguments. In JS, the default values for both should be
`null`, while they should both be `nil` in Ruby. Choose a comparable value if
coding in other languages.

When instantiating a new `Node`, the arguments in order should be: `value`,
`next`.

```txt
node = new Node()
node.value
=> null or nil
node.next
=> null or nil

node = new Node('hi', new Node('bye'))
node.value
=> 'hi'
node.next
=> Instance of Node with value of 'bye'
```

### 2. Define the `LinkedList` Class

The `LinkedList` class tracks the `head` of the list, so we know where it
begins. It should have one attribute: `head`. Provide a default value for `head`
of `null` or `nil`, or some other falsy value.

```txt
node = new Node()
list = new LinkedList(node)
list.head
=> Instance of Node

emptyList = new LinkedList()
list.head
=> null or nil
```

### 3. Spend a Few Minutes Playing With Your Linked List

See if you can recreate the following Arrays as Linked Lists using your classes,
where the 0th element denotes the `head` of the list:

```txt
characters = ['Hamtaro', 'Walter White']
drinks = ['Coffee', 'Manhattan', 'Brandy Sour']
```

You can test this manually like so:

```txt
head = new Node('hi again', new Node('but why?'))
list = new LinkedList(head)
print list.head.value
print list.head.next.value
print list.head.next.next
```

### 4. Add `iterate` Method to `LinkedList`

For now, we'll build part of the `iterate` method (but not all of it). The
`iterate` method traverses the entire `LinkedList`. To ensure that it's working,
we'll print the value of each `Node`. Later we'll remove this functionality and
update the method to take a callback.

Remember, the `head` is the first `Node` in the list, and the next one is stored
in its `next` attribute. We can go to each `Node` by visiting all of the
`next`s. When `next` is equal to a falsy value, such as `null` or `nil`, we've
reached the end of the list. At the end of the iteration, return the `head`.

```txt
head = new Node('hi again', new Node('but why?'))
list = new LinkedList(head)
list.iterate()
=> 'hi again'
=> 'but why?'
=> Node with value 'hi again'
```

### 5. Modify the `iterate(callback)` Method to Take a Callback

Change the `iterate` method, so that it takes a callback (a function) as an
argument.

Replace the print statements in the `iterate` method with a call to the
callback. When calling the callback, provide the current Node as an argument to
the callback. You can test if this is working by calling `iterate` on the list
with a callback that prints the value of each Node.

```txt
function printNode(node):
  print node.value

head = new Node('hi again', new Node('but why?'))
list = new LinkedList(head)
list.iterate(printNode)
=> 'hi again'
=> 'but why?'
=> Node with value 'hi again'
```

**Hint**: Rubyists might be interested in learning about passing blocks and
using [`yield`][yield] to implement the `iterate` method. Your Ruby
implementation should accept a block rather than a callback function:

```rb
head = Node.new('hi again', Node.new('but why?'))
list = LinkedList.new(head)
list.iterate do |node|
  puts node.value
end
```

[yield]: https://www.brainstobytes.com/ruby-iterators-and-the-yield-keyword-with-examples/

### 6. Add `print` method to `LinkedList`

The `print` method should print each node value on its own line. Use the
`iterate` method in the `print` method.

```txt
head = new Node('hi again', new Node('but why?'))
list = new LinkedList(head)
list.print()
=> 'hi again'
=> 'but why?'
```

### 7. Add `find(target)` method to `LinkedList`

The `find` method searches for a `Node` with the `target` value. If the `Node`
is found, it returns that `Node`. Otherwise, it returns a falsy value such as
`null` or `nil`. Use the `iterate` method to keep your code short and DRY.

```txt
head = new Node('hi again', new Node('but why?'))
list = new LinkedList(head)
list.find('but why?')
=> Node with value 'but why?'

list.find('tell me secrets')
=> null or nil, etc.
```

### 8. Add `addFirst(node)` method to `LinkedList`

`addFirst` takes a Node as an argument and adds it as the `head` of the Linked
List. No existing Nodes are removed.

This method adds only 1 Node to the list.

```txt
head = new Node('hi again', new Node('but why?'))
list = new LinkedList(head)
list.addFirst(new Node('I am first now'))
list.print()
=> 'I am first now'
=> 'hi again'
=> 'but why?'
```

### 9. Add `addLast(node)` method to `LinkedList`

`addLast` takes a Node as an argument and adds it at the end of the Linked List
(i.e. it will be the tail). No existing Nodes are removed. The `iterate` method
can help you here.

This method adds only 1 Node to the list.

```txt
head = new Node('hi again', new Node('but why?'))
list = new LinkedList(head)
list.addLast(new Node('I am last'))
list.print()
=> 'hi again'
=> 'but why?'
=> 'I am last'
```

### 10. Add `removeFirst` method to `LinkedList`

`removeFirst` removes the first (head) Node in the list and returns the node
that was removed.

Hint: Try not to overthink this. Removing the head takes one line of code.
You'll need a little bit more code to handle returning the node that was
removed, however.

```txt
head = new Node('hi again', new Node('but why?'))
list = new LinkedList(head)
list.removeFirst()
=> Node with value 'hi again'
list.print()
=> 'but why?'
```

### 11. Add `removeLast` method to `LinkedList`

`removeLast` removes the last (tail) Node in the list and returns the removed
Node.

Hint: The `iterate` method might be helpful here.

```txt
head = new Node('hi again', new Node('but why?'))
list = new LinkedList(head)
list.removeLast()
=> Node with value 'but why?'
list.print()
=> 'hi again'
```

### 12. Add `replace(index, node)` to `LinkedList`

Replace the Node at the given `index` with the given `node`. `replace` should
work on all Node indexes. Nodes are zero-indexed.

Don't worry about handling invalid indexes, such as -1 or those that go beyond
the size of the list.

Return the inserted Node.

Hint: The `iterate` method might be helpful here. You may wish to modify it by
adding the ability to count, or you can declare the count within `replace` and
update it in the callback passed to `iterate`. Or you can create an
`iterate_with_count` method and use that (and that method can call the `iterate`
method). So many options!

```txt
head = new Node('one', new Node('two', new Node('three')))
list = new LinkedList(head)
list.replace(0, '1')
=> Node with value '1'
// list is now '1' -> 'two' -> 'three'

list.replace(1, '2')
=> Node with value '2'
// list is now '1' -> '2' -> 'three'

list.replace(2, '3')
=> Node with value '3'
// list is now '1' -> '2' -> '3'
```

### 13. Add `insert(index, node)` to `LinkedList`

Insert the given `node` at the given `index` in the `LinkedList`. No nodes
should be removed or replaced! This method inserts only 1 Node into the list.

Ensure you can handle all valid `index` values: 0 to last index + 1 in list.
Don't worry about invalid index values.

Hint: `iterate` may be helpful once more.

```txt
head = new Node('one', new Node('two', new Node('three')))
list = new LinkedList(head)
list.insert(1, new Node('inserted at 1'))
// list is now 'one' -> 'inserted at 1' -> 'two' -> 'three'
```

```txt
head = new Node('one', new Node('two', new Node('three')))
list = new LinkedList(head)
list.insert(0, new Node('inserted at 0'))
// list is now 'inserted at 0' -> 'one' -> 'two' -> 'three'
```

```txt
head = new Node('one', new Node('two', new Node('three')))
list = new LinkedList(head)
list.insert(3, new Node('inserted at 3'))
// list is now 'one' -> 'two' -> 'three' -> 'inserted at 3'
```

### 14. Add `remove(index)` to `LinkedList`

Remove the `Node` at the given `index` and return the removed `Node`. Don't
worry about invalid indices, such as -1 or those that go beyond the size of the
list.

Hint: Good ol' `iterate`...again!

```txt
head = new Node('one', new Node('two', new Node('three')))
list = new LinkedList(head)

list.remove(1)
=> Node with value 'two'
// list is now 'one' -> 'three'

list.remove(1)
=> Node with value 'three'
// list is now 'one'

list.remove(0)
=> Node with value 'one'
// list is empty :(
```

### 15. Add `clear` to `LinkedList`

Clear the linked list.

```txt
head = new Node('one', new Node('two', new Node('three')))
list = new LinkedList(head)

list.clear()
list.print()
// nothing happens because it's empty
list.head
=> null or nil
```

## Before you start coding

1. Rewrite the problem in your own words
2. Validate that you understand the problem
3. Write your own test cases
4. Pseudocode
5. Code!

**_And remember, don't run our tests until you've passed your own!_**

## How to run your own tests

### Ruby

1. `cd` into the ruby folder
2. `ruby <filename>.rb`

### JavaScript

1. `cd` into the javascript folder
2. `node <filename>.js`

## How to run our tests

### Ruby

1. `cd` into the ruby folder
2. `bundle install`
3. `rspec`

### JavaScript

1. `cd` into the javascript folder
2. `npm i`
3. `npm test`
