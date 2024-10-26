# Trabajo Estructuras de datos:

Nombres: Ana Sofia Ossa Betancur, Alejandro Ramirez Huertas

Las primeras cinco alturas al correr el código son las siguientes:
![344fb2c9-cf1a-43e8-af62-e3d8d25a4eae](https://github.com/user-attachments/assets/a9995799-0682-467c-a97b-ef1a92de75a8)
![10bc734a-bfa5-4f73-af90-5f65434abc00](https://github.com/user-attachments/assets/81325ca0-3203-4d92-b16a-aa48096ec388)
![e6665086-eac9-4ef7-a843-372e10cb561e](https://github.com/user-attachments/assets/eccd1483-8bfb-4bb5-992a-d72a1f1cb2aa)
![408f6d46-7905-441c-87b4-3e867603d8a3](https://github.com/user-attachments/assets/b365269e-b356-4572-8359-8f6d2e557899)
![f3d23083-16aa-484d-a40f-3c5e07f018ff](https://github.com/user-attachments/assets/1ce607f1-e5f5-4773-9381-be92ac526a65)

## Conclusiones:
Además de estas 5, contando con las demás veces que corrimos el código, obtuvimos un promedio de 13.8 de la altura. La cual oscila entre 9 y 20, por lo que podemos concluir que este método de recorrer el vector aleatoriamente e insertar su contenido en el árbol, optimiza recorridos futuros del árbol, pues el máximo número de niveles que puede alcanzar de altura es 100, y el promedio del experimento nos rojó resultados muy apartados de este. Posteriormente se realizó el experimento con 1000 elementos, la altura promedio dio 22.5 después de 20 ejecuciones del código. El máximo de niveles sería 1000, y no se llegó ni al 3% de esta altura. Por tanto es un muy buen método de optimización incluso para un número grande de datos.

Código:
```c++

#include <iostream>
#include <cassert>
#include <stdbool.h>
#include <time.h>
#include <stdlib.h>
#include <stdio.h>
#include <vector>

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

 public :

  int altura() {
    return altura(root);  // Llamada a la función privada recursiva
  }
};

int main() {
    
    vector<string> ciudadesVector = {
        "Ámsterdam", "Ankara", "Atenas", "Auckland", "Bangkok", "Barcelona", "Beirut", "Belgrado", "Berlín", "Bogotá",
        "Boston", "Bratislava", "Bruselas", "Budapest", "Buenos Aires", "Cairo", "Calcuta", "Canberra", "Caracas", "Casablanca",
        "Chicago", "Ciudad de México", "Copenhague", "Dakar", "Damasco", "Dublín", "Dubái", "Edimburgo", "Estambul", "Estocolmo",
        "Fráncfort", "Ginebra", "Glasgow", "Guadalajara", "Hamburgo", "Helsinki", "Hong Kong", "Honolulu", "Houston", "Islamabad",
        "Jakarta", "Jerusalén", "Johannesburgo", "Kabul", "Kampala", "Katmandú", "Kiev", "Kigali", "Kingston", "Kuala Lumpur",
        "La Habana", "Lagos", "Lima", "Lisboa", "Londres", "Los Ángeles", "Luanda", "Madrid", "Managua", "Manila",
        "Marrakech", "Marsella", "Melbourne", "México D.F.", "Miami", "Milán", "Montevideo", "Moscú", "Múnich", "Nairobi",
        "Nueva Delhi", "Nueva York", "Oslo", "Ottawa", "Panamá", "París", "Pekín", "Perth", "Praga", "Quito",
        "Rabat", "Reikiavik", "Río de Janeiro", "Roma", "San Francisco", "San José", "San Juan", "San Salvador", "Santiago de Chile", "Santo Domingo",
        "São Paulo", "Seúl", "Shanghái", "Singapur", "Sídney", "Sofía", "Tiflis", "Tokio", "Toronto", "Varsovia"
    };

    srand(time(NULL));
    int r;
    BST<string, int> ciudades;
    
    while(1){
     if(ciudadesVector.size()==0){
      break;
     }
     else{
       r=rand() % ciudadesVector.size();
       ciudades.insert(ciudadesVector.at(r),r);
       ciudadesVector.erase(ciudadesVector.begin() + r);
     }
    }
    
    
   ciudades.print();
    cout << endl;
    cout << endl;
    cout << "INORDER : " <<  endl;
    cout << endl;
    ciudades.inorder();
    cout << endl;
    cout << endl;
    cout << "POSORDER : " <<  endl;
    cout << endl;
    ciudades.posorder();
    cout << endl;
    cout << endl;
    cout << "PREORDER : " <<  endl;
    cout << endl;
    ciudades.preorder();
    cout << endl;
    cout << endl;

    
    cout << "La altura del arbol es: " << ciudades.altura() << endl;
}
```
