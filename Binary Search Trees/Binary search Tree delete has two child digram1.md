```mermaid
%%{init: {'theme': 'dark', 'themeVariables': { 'nodeTextColor': '#FFFFFF'}}}%%
graph TD
    subgraph Initial[Initial Tree]
        A0[50] --> B0[30]
        A0 --> C0[70]
        B0 --> D0[20]
        B0 --> E0[40]
        C0 --> F0[60]
        C0 --> G0[80]
        F0 --> H0[55]
        F0 --> I0[65]
    end

    subgraph Delete30[After deleting 30]
        A1[50] --> B1[40]
        A1 --> C1[70]
        B1 --> D1[20]
        C1 --> F1[60]
        C1 --> G1[80]
        F1 --> H1[55]
        F1 --> I1[65]
    end

    subgraph Delete70[After deleting 70]
        A2[50] --> B2[30]
        A2 --> C2[80]
        B2 --> D2[20]
        B2 --> E2[40]
        C2 --> F2[60]
        F2 --> H2[55]
        F2 --> I2[65]
    end

    subgraph Delete60[After deleting 60]
        A3[50] --> B3[30]
        A3 --> C3[70]
        B3 --> D3[20]
        B3 --> E3[40]
        C3 --> F3[65]
        C3 --> G3[80]
        F3 --> H3[55]
    end

    style B0 fill:#FF5733,stroke:#FFFFFF,stroke-width:2px
    style C0 fill:#3357FF,stroke:#FFFFFF,stroke-width:2px
    style F0 fill:#33FF57,stroke:#FFFFFF,stroke-width:2px

    style B1 fill:#33FF57,stroke:#FFFFFF,stroke-width:2px
    style C2 fill:#33FF57,stroke:#FFFFFF,stroke-width:2px
    style F3 fill:#33FF57,stroke:#FFFFFF,stroke-width:2px
```


### Deleting 30:
- Node to delete: 30 (orange in Initial Tree)
- In-order successor: 40 (right child of 30)
- Process:
    1. Find 40 as the successor (smallest in the right subtree of 30)
    2. Replace 30's data with 40
    3. Update 30's right pointer to 40's right child (null in this case)
    4. Delete the original 40 node
- Result: 40 takes 30's place, and its left child (20) remains in place

### Deleting 70:
- Node to delete: 70 (blue in Initial Tree)
- In-order successor: 80 (right child of 70)
- Process:
    1. Find 80 as the successor (smallest in the right subtree of 70)
    2. Replace 70's data with 80
    3. Update 70's right pointer to 80's right child (null in this case)
    4. Delete the original 80 node
- Result: 80 takes 70's place, and 70's left subtree (60 and its children) remains unchanged

### Deleting 60:
- Node to delete: 60 (green in Initial Tree)
- In-order successor: 65 (smallest in the right subtree of 60)
- Process:
    1. Find 65 as the successor
    2. Replace 60's data with 65
    3. Update 60's right pointer to 65's right child (null in this case)
    4. Delete the original 65 node
- Result: 65 takes 60's place, and 60's left child (55) remains in place



<div style="color: #66CDAA;">
    <strong>Key points:</strong>
    <ul>
        <li><strong>In each case, we find the smallest node in the right subtree of the node to delete.</strong></li>
        <li><strong>We replace the data of the node to delete with the data from the successor.</strong></li>
        <li><strong>We then remove the successor from its original position.</strong></li>
        <li><strong>This process maintains the BST property: all nodes in the left subtree are smaller, and all nodes in the right subtree are larger than the new node.</strong></li>
    </ul>
</div>

