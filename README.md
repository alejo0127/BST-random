#include <iostream>
#include <cassert>
#include <stdbool.h>

using namespace std;

template <typename K, typename V>
class BST {
 private:
  class Node {
   private:
    K key;
    V value;
    Node* left;
    Node* right;
   public:
    Node() : key(), value(), left(nullptr), right(nullptr) {}
    Node(K k, V v) : key(k), value(v), left(nullptr), right(nullptr) {}
    K getKey() { return key; }
    V getValue() { return value; }
    bool hasLeft() { return left != nullptr; }
    bool hasRight() { return right != nullptr; }
    void setLeft(Node* n) { left = n; }
    void setRight(Node* n) { right = n; }
    Node* getLeft(){ return left;}
    Node* getRight(){ return right;}
    void print(Node *n){
      cout<<n->getKey()<<" "<<n->getValue()<<endl;
      if(n->hasLeft()){
        cout<<n->getKey()<<"\'s left: "<<endl;
        print(n->getLeft());
      }
      if(n->hasRight()){
        cout<<n->getKey()<<"\'s right: "<<endl;
        print(n->getRight());
      }
    }
  };

 private:
  Node* root;
  unsigned int size;

  // Función para insertar un nodo en el BST
  void insert(K key, V value, Node* n) {
    if (key < n->getKey()) {
      if (n->hasLeft()) {
        insert(key, value, n->getLeft());
      } else {
        Node* x = new Node(key, value);
        n->setLeft(x);
        size++;
      }
    } else if (n->getKey() < key) {
      if (n->hasRight()) {
        insert(key, value, n->getRight());
      } else {
        Node* x = new Node(key, value);
        n->setRight(x);
        size++;
      }
    } else {
      // key repetido
    }
  }

  // Recorridos del árbol
  void preorder(Node * n){
    if(n == nullptr) return;
    cout << n->getKey() << " ";
    preorder(n->getLeft());
    preorder(n->getRight());
  }

  void inorder(Node * n){
    if(n == nullptr) return;
    inorder(n->getLeft());
    cout << n->getKey() << " ";
    inorder(n->getRight());
  }

  void posorder(Node * n){
    if(n == nullptr) return;
    posorder(n->getLeft());
    posorder(n->getRight());
    cout << n->getKey() << " ";
  }

  
  int altura(Node* n) {
   
    if(n==nullptr){
      return 0;
    }

    int alturaIzquierda = altura(n->getLeft());
    int alturaDerecha = altura(n->getRight());

    
    return 1 + max(alturaIzquierda, alturaDerecha);
  }

 public:
  BST() : root(nullptr), size(0) {}
  
  unsigned int getSize() { return size; }
  bool empty() { return root == nullptr; }
  
  void insert(K key, V value) {
    if (empty()) {
      root = new Node(key, value);
      size++;
    } else {
      insert(key, value, root);
    }
  }

  void print() {
    assert(!empty() && "vacío");
    cout<<"Arbol:\nRaiz:"<<root->getKey()<<" "<<root->getValue()<<endl;
    if(root->hasLeft()) {
      cout<<root->getKey()<<"\'s left: "<<endl;
      root->print(root->getLeft());
    }
    if(root->hasRight()) {
      cout<<root->getKey()<<"\'s right: "<<endl;
      root->print(root->getRight());
    }
  }

  void preorder() {
    if (root == nullptr) {
      cout << "vacio" << endl;
    } else {
      preorder(root);
    }
  }

  void inorder() {
    if (root == nullptr) {
      cout << "vacio" << endl;
    } else {
      inorder(root);
    }
  }

  void posorder() {
    if (root == nullptr) {
      cout << "vacio" << endl;
    } else {
      posorder(root);
    }
  }

  // Función pública para obtener la altura del BST
  int altura() {
    return altura(root);  // Llamada a la función privada recursiva
  }
};

int main() {
    cout << "hola" << endl;
    
    BST<string, int> ciudades;
    ciudades.insert("pereira", 1);
    ciudades.insert("manizales", 2);
    ciudades.insert("bogota", 3);
    ciudades.insert("cali", 4);
    ciudades.insert("piendamo", 5);
    ciudades.insert("guacari", 6);
    ciudades.insert("armenia", 7);
    ciudades.insert("leguizamo",8);
    
    ciudades.print();
    ciudades.inorder();
    cout << endl;
    ciudades.posorder();
    cout << endl;
    ciudades.preorder();
    cout << endl;

    
    cout << "La altura del arbol es: " << ciudades.altura() << endl;
}
