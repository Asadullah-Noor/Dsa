# Dsa
ASSIGNMENT 4

#include <iostream>
using namespace std;

struct product {
    int pid;
    int pr;
    float wgt;
    string name;
    string category;

    product(int id, string name, int pr, float wgt, string ctg) {
        pid = id;
        this->name = name;
        this->pr = pr;
        this->wgt = wgt;
        this->category = ctg;
    }
};

struct Node {
    product key;
    Node* left;
    Node* right;

    Node(product pr) : key(pr), left(nullptr), right(nullptr) {}
};

class BST {
    Node* root;

    Node* insert(Node* root, product pd) {
        if (!root) return new Node(pd);
        if (pd.pid < root->key.pid) {
            root->left = insert(root->left, pd);
        } else {
            root->right = insert(root->right, pd);
        }
        return root;
    }

    void inorder(Node* root) {
        if (!root) return;
        inorder(root->left);
        cout << "Product ID: " << root->key.pid << endl;
        cout << ", Name: " << root->key.name << endl;
        cout << ", Price: " << root->key.pr << endl;
        cout << ", Weight: " << root->key.wgt << endl;
        cout << ", Category: " << root->key.category << endl;
        inorder(root->right);
    }

    void search(Node* root, string category) {
        if (!root) return;
        search(root->left, category);
        if (root->key.category == category) {
            cout << "Product ID: " << root->key.pid << endl;
            cout << ", Name: " << root->key.name << endl;
            cout << ", Price: " << root->key.pr << endl;
            cout << ", Weight: " << root->key.wgt << endl;
            cout << ", Category: " << root->key.category << endl;
        }
        search(root->right, category);
    }

public:
    BST() : root(nullptr) {}

    void insert(product pr) {
        root = insert(root, pr);
    }

    void search(string category) {
        cout << "Products in Category: " << category << endl;
        search(root, category);
    }

    void display() {
        inorder(root);
    }
};

int main() {
    BST p;
    p.insert(product(103, "Table", 1500, 2.5, "furniture"));
    p.insert(product(104, "Chair", 1500, 2.5, "furniture"));
    p.insert(product(105, "Laptop", 1500, 2.5, "Electronics"));
    p.insert(product(106, "Mobile", 1500, 2.5, "Android"));

    p.display();

    string ct = "Android";
    cout << "The category name is " << ct << endl;
    p.search(ct);

    return 0;
}
