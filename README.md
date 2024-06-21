### Kelas `Node`
```java
class Node {
    int data;
    Node left, right;

    public Node(int item) {
        data = item;
        left = right = null;
    }
}
```
- **`Node`**: Kelas ini merepresentasikan sebuah node dalam pohon biner.
  - `int data`: Menyimpan nilai data dari node.
  - `Node left, right`: Menyimpan referensi ke anak kiri dan anak kanan dari node tersebut.
  - Konstruktor `Node(int item)`: Menginisialisasi `data` dengan nilai yang diberikan (`item`) dan menetapkan `left` dan `right` menjadi `null`.

### Kelas `BinaryTree`
```java
class BinaryTree {
    Node root;

    BinaryTree() {
        root = null;
    }
```
- **`BinaryTree`**: Kelas ini merepresentasikan pohon biner.
  - `Node root`: Menyimpan referensi ke root (akar) dari pohon biner.
  - Konstruktor `BinaryTree()`: Menginisialisasi `root` menjadi `null`.

#### Metode `insert`
```java
    void insert(int data) {
        root = insertRec(root, data);
    }

    Node insertRec(Node root, int data) {
        if (root == null) {
            root = new Node(data);
            return root;
        }
        if (data < root.data)
            root.left = insertRec(root.left, data);
        else if (data > root.data)
            root.right = insertRec(root.right, data);

        return root;
    }
```
- **`insert(int data)`**: Metode ini menyisipkan nilai `data` ke dalam pohon biner dengan memanggil metode rekursif `insertRec`.
- **`insertRec(Node root, int data)`**: Metode rekursif yang menyisipkan nilai `data` ke dalam posisi yang tepat dalam pohon:
  - Jika `root` adalah `null`, node baru dengan `data` dibuat dan dikembalikan sebagai root.
  - Jika `data` lebih kecil dari `root.data`, maka disisipkan ke subpohon kiri.
  - Jika `data` lebih besar dari `root.data`, maka disisipkan ke subpohon kanan.

#### Metode `inorder`
```java
    void inorder() {
        inorderRec(root);
    }

    void inorderRec(Node root) {
        if (root != null) {
            inorderRec(root.left);
            System.out.print(root.data + " ");
            inorderRec(root.right);
        }
    }
```
- **`inorder()`**: Memulai traversal inorder dengan memanggil metode rekursif `inorderRec`.
- **`inorderRec(Node root)`**: Metode rekursif untuk traversal inorder:
  - Jika `root` tidak `null`, kunjungi subpohon kiri, cetak `root.data`, kemudian kunjungi subpohon kanan.

#### Metode `bfs`
```java
    void bfs() {
        if (root == null)
            return;

        Queue<Node> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            Node tempNode = queue.poll();
            System.out.print(tempNode.data + " ");

            if (tempNode.left != null)
                queue.add(tempNode.left);

            if (tempNode.right != null)
                queue.add(tempNode.right);
        }
    }
```
- **`bfs()`**: Melakukan traversal BFS pada pohon:
  - Jika `root` adalah `null`, keluar dari metode.
  - Buat `Queue` dan tambahkan `root` ke dalam queue.
  - Selama queue tidak kosong, ambil node dari depan queue, cetak `data`-nya, dan tambahkan anak kiri dan kanannya (jika ada) ke dalam queue.

### Metode `main`
```java
    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        Scanner scanner = new Scanner(System.in);
        char choice;
        do {
            System.out.print("Masukkan angka node: ");
            int data = scanner.nextInt();
            tree.insert(data);

            System.out.print("Apakah Anda ingin memasukkan node lagi? (y/n): ");
            choice = scanner.next().charAt(0);
        } while (choice == 'y' || choice == 'Y');

        System.out.println("Traversal inorder dari tree:");
        tree.inorder();

        System.out.println("\nTraversal BFS dari tree:");
        tree.bfs();
    }
}
```
- **`main(String[] args)`**: Metode utama yang menjalankan program:
  - Membuat instance dari `BinaryTree`.
  - Menggunakan `Scanner` untuk membaca input dari pengguna.
  - Menggunakan loop `do-while` untuk terus meminta pengguna memasukkan nilai node dan menambahkannya ke pohon sampai pengguna memilih untuk berhenti (`choice` != `y` atau `Y`).
  - Setelah semua node dimasukkan, mencetak traversal inorder dan BFS dari pohon.
