Here’s the updated Mermaid diagram for the `delete_child_helper` function:

```mermaid
flowchart TD
    A[Start Deleting Leaf Node] --> B{Node Found?}
    B -- No --> C[Print 'Node not found'] --> D[End]
    B -- Yes --> E{Is Node the Root?}
    E -- Yes --> F[Delete Root] --> G[Set Root to NULL] --> H[Print 'Root node deleted'] --> D
    E -- No --> I[Find Parent of Node] --> J{Parent Found?}
    J -- No --> C
    J -- Yes --> K{Is Node Left Child?}
    K -- Yes --> L[Set Parent's Left Pointer to NULL] --> M[Delete Node] --> N[Print 'Node deleted'] --> D
    K -- No --> O[Set Parent's Right Pointer to NULL] --> M
```

This flowchart illustrates how the `delete_child_helper` function proceeds, checking whether the node is the root, adjusting parent pointers, and deleting the node when it's a leaf.