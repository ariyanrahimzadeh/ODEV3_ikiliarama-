ikili arama odevi ARIAN RAHIMZADEH ABDI  20222013275





**(agac olusturma)**

&nbsp;

\#include <iostream>

\#include <queue>

using namespace std;



enum TraversalMode {

&nbsp;   PRE\_ORDER,

&nbsp;   POST\_ORDER

};



struct Node {

&nbsp;   int data;

&nbsp;   Node\* left;

&nbsp;   Node\* right;

&nbsp;   Node(int val) : data(val), left(nullptr), right(nullptr) {}

};



class BinarySearchTree {

private:

&nbsp;   Node\* root;

&nbsp;   // ... yardimci (private) fonksiyonlar buraya gelecek

public:

&nbsp;   BinarySearchTree() : root(nullptr) {}

&nbsp;   // ... Ana (public) fonksiyonlar buraya gelecek

};









**(agaca eleman ekleme)**





Node\* insertRecursive(Node\* node, int value) {

&nbsp;   if (node == nullptr) {

&nbsp;       return new Node(value);

&nbsp;   }

&nbsp;   if (value < node->data) {

&nbsp;       node->left = insertRecursive(node->left, value);

&nbsp;   } else if (value > node->data) {

&nbsp;       node->right = insertRecursive(node->right, value);

&nbsp;   }

&nbsp;   return node;

}



// Public :

void insert(int value) {

&nbsp;   root = insertRecursive(root, value);

}









**(DFS)**



void dfsRecursive(Node\* node, TraversalMode mode) {

&nbsp;   if (node == nullptr) return;





&nbsp;   if (mode == PRE\_ORDER) cout << node->data << " ";

&nbsp;   

&nbsp;   dfsRecursive(node->left, mode);  // Solu gez

&nbsp;   dfsRecursive(node->right, mode); // Sağı gez

&nbsp;   



&nbsp;   if (mode == POST\_ORDER) cout << node->data << " ";

}





void traverseDFS(TraversalMode mode) {

&nbsp;   dfsRecursive(root, mode);

&nbsp;   cout << endl;

}







**(BFS)**





void traverseBFS() {

&nbsp;   if (root == nullptr) return;

&nbsp;   

&nbsp;   queue<Node\*> q;

&nbsp;   q.push(root);



&nbsp;   while (!q.empty()) {

&nbsp;       Node\* current = q.front();

&nbsp;       q.pop();

&nbsp;       cout << current->data << " ";



&nbsp;       if (current->left != nullptr) q.push(current->left);

&nbsp;       if (current->right != nullptr) q.push(current->right);

&nbsp;   }

&nbsp;   cout << endl;

}







**(silme)**



**void deleteSubtreeRecursive(Node\* node) {**

    **if (node == nullptr) return;**

    **deleteSubtreeRecursive(node->left);**

    **deleteSubtreeRecursive(node->right);**

    **delete node; // Bellekten sil**

**}**



**Node\* deleteNodeWithSubtreeRecursive(Node\* node, int value) {**

    **if (node == nullptr) return nullptr;**



    **if (value < node->data) {**

        **node->left = deleteNodeWithSubtreeRecursive(node->left, value);**

    **} else if (value > node->data) {**

        **node->right = deleteNodeWithSubtreeRecursive(node->right, value);**

    **} else {**

        **// Düğüm bulundu, altındakileri ve kendisini sil**

        **deleteSubtreeRecursive(node->left);**

        **deleteSubtreeRecursive(node->right);**

        **delete node;**

        **return nullptr;**

    **}**

    **return node;**

**}**



**void removeNodeAndSubtree(int value) {**

    **root = deleteNodeWithSubtreeRecursive(root, value);**

**}**







**(BONUS SORU)**



Node\* findMin(Node\* node) {

&nbsp;   while (node->left != nullptr) node = node->left;

&nbsp;   return node;

}



Node\* deleteNodePreserveOrderRecursive(Node\* node, int value) {

&nbsp;   if (node == nullptr) return nullptr;





&nbsp;   if (value < node->data) {

&nbsp;       node->left = deleteNodePreserveOrderRecursive(node->left, value);

&nbsp;   } else if (value > node->data) {

&nbsp;       node->right = deleteNodePreserveOrderRecursive(node->right, value);

&nbsp;   } else {

&nbsp; 

&nbsp;       if (node->left == nullptr) {

&nbsp;           Node\* temp = node->right;

&nbsp;           delete node;

&nbsp;           return temp;

&nbsp;       } else if (node->right == nullptr) {

&nbsp;           Node\* temp = node->left;

&nbsp;           delete node;

&nbsp;           return temp;

&nbsp;       }



&nbsp;               Node\* temp = findMin(node->right);

&nbsp;       

&nbsp;       

&nbsp;       node->data = temp->data;

&nbsp;       

&nbsp;       node->right = deleteNodePreserveOrderRecursive(node->right, temp->data);

&nbsp;   }

&nbsp;   return node;

}



void removeNodeKeepOrder(int value) {

&nbsp;   root = deleteNodePreserveOrderRecursive(root, value);

}

