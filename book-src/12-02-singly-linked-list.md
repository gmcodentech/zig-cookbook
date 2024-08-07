# Singly Linked List

[Singly linked list] contains nodes linked together. The list contains:
- `head`, head of the list, used for traversal.
- `tail`, tail of the list, used for fast add.
- `len`, length of the list

Operations that can be performed on singly linked lists include:
- Insertion O(1)
- Deletion O(n), which is the most complex since it needs to maintain head/tail pointer.
- Traversal O(n)

```zig
{{#include ../src/12-02.zig }}
```

[Singly linked list]: https://en.wikipedia.org/wiki/Linked_list
