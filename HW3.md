
```Java
public  void revert(){
        if (head != null && head.next != null)
            revert(head.next, head);
}
private void revert(Node node, Node nodeNext){
        if (node.next == null) {
            head = node;
        }else {
            revert(node.next, node);
        }
        node.next = nodeNext;
        nodeNext.next = null;
}
```