### 删除链表中倒数第n个节点
1、思路1：定义两个指针slow，fast。它们之间间隔n-1个节点，再使slow，fast同时移动，直到其中一个最先到达链表尾部为止。（注意一些边界条件）

/**
 * Definition for ListNode.
 */

class Node2 {
    int val;
    Node2 next;

    Node2(int val) {
        this.val = val;
        this.next = null;
    }

    public void add(int val) {
        if (this.next == null) {
            this.next = new Node2(val);
        } else {
            this.next.add(val);
        }
    }

    public void print() {
        System.out.println(val);
        if (this.next != null) {
            this.next.print();
        }
    }
}

/**
 * Created by wangbingbing on 2017/5/15.
 */
public class LinkDemo2 {

    /**
     * 删除倒数第n个节点，如果超出链表长度，则不删除任何节点
     * 
     * @param head
     *            : The first node of linked list.
     * @param n
     *            : An integer.
     * @return: The head of linked list.
     */
    private static Node2 removeNthFromEnd(Node2 head, int n) {
        if (n <= 0 || head == null) {// 如果n为非正数 或者 头节点是空，则直接返回头结点
            return head;
        }
        Node2 slow = head;// 指向头结点
        Node2 fast = head;// 指向头结点
        while (fast.next != null && n > 0) {// fast指针先移动到第n个结点，或者尾结点
            fast = fast.next;
            n--;
        }
        if (fast.next == null) {// 如果fast.next此时为空，则fast移动到了尾节点
            if (n > 1) {// 如果此时n还大于1，说明n的长度已经越界了，直接返回头结点
                return head;
            }
            if (n == 1) {// 如果此时n还为1，说明要删除头结点，返回头结点的下一个结点
                return head.next;
            }
        }
        while (fast.next != null) {// 如果fast.next不为空，继续移动，直到尾结点
            fast = fast.next;
            slow = slow.next;
        }
        slow.next = slow.next.next;// 因为slow和fast中间隔着n-1个结点，所以fast到尾结点时，slow正好在倒数第n个结点上
        return head;
    }

    public static void main(String[] args) {
        Node2 node = new Node2(0);
        node.add(1);
        node.add(2);
        node.add(3);
        node.add(4);
        node.add(5);
        removeNthFromEnd(node, 3).print();
    }
}

2、思路2：先转置，再删除，再转置

package link;

/**
 * Created by wangbingbing on 2017/5/15.
 */
class Node {
    private String data;
    private Node next;

    public Node(String data) {
        this.data = data;
    }

    public void addNode(Node node) {
        if (this.next == null) {
            this.next = node;
        } else {
            this.next.addNode(node);
        }
    }

    public Node reverse(Node root) {
        if (root == null || root.next == null) {
            return root;
        } else {
            Node temp = root.next;
            Node reverseRoot = this.reverse(root.next);

            temp.next = root;
            root.next = null;
            return reverseRoot;
        }
    }

    public void print() {
        System.out.println(this.data);
        if (this.next != null) {
            this.next.print();
        }
    }

    public void remove(int index, int target) {
        if (index < target && this.next != null) {
            if (index == target - 1) {
                this.next = this.next.next;
            } else {
                index++;
                this.next.remove(index, target);
            }
        }
    }
}

class Link {
    private Node root;

    public void add(String data) {
        Node node = new Node(data);
        if (root == null) {
            this.root = node;
        } else {
            this.root.addNode(node);
        }
    }

    public void reverse() {
        this.root = this.root.reverse(root);
    }

    public void print() {
        if (root != null) {
            this.root.print();
        } else {
            System.out.println("NULL");
        }
    }

    public void removeIndex(int target) {
        this.root.remove(1, target);
    }
}

public class LinkDemo {
    public static void main(String[] args) {
        Link link = new Link();
        link.add("0");
        link.add("1");
        link.add("2");
        link.add("3");
        link.add("4");
        link.add("5");
        link.add("6");
        link.add("7");
        link.add("8");
        link.add("9");
        link.reverse();
        link.removeIndex(4); //删除倒数第4个节点 
        link.reverse();
        link.print();
    }
}
