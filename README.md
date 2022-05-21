# Proyecto-de-EDA
Hola,aqui escribe los avances del codigo

NOTAS:
Notacion Infija a postfija

1) Insertar desde el teclado
    Ej:
        [ 1 + 2 + 3 * 4 - 2 / 6 ]

        Programa:

        //Simbologia evaluada por prioridad.
        Acomodar los numeros y operadores en una pila.
        ->pila = Notacion Infija

        ->cola = Notacion postfija


        ->IMPLEMENTANDO las funciones de a lista ligada:
                 - Insertar por head            - Insertar por tail
                 - Eliminar por head            - Eliminar por tail
                                - Imprimir

    IMPRIMIR:
     - Notacion Infija 

     - Notacion Postfija





----------------------------------------------------------------------------------------------------------------------------

Nodo.h
#ifndef __NODO_H__
#define __NODO_H__

typedef int Data;

typedef struct Nodo{
    Data dato;
    struct Nodo *sig;
    struct Nodo *ant;
} Nodo;
//Definida en una sola instruccion la estructura;

Nodo *crear_nodo(Data d);
void borrar_nodo(Nodo *n);
void actualizar_nodo(Nodo *n, Data d);

#endif


----------------------------------------------------------------------------------------------------------------------------

Cola.h
#ifndef __COLA_H__
#define __COLA_H__
#include "Nodo.h"
#include <stdbool.h>
struct _cola
{
    Nodo* _frente;
    Nodo* _final;
    int lon;
};
typedef struct _cola cola;

cola* cola_vacia();
bool encolar(cola*,Data);//RECIBE UN APUNTADOR A LA `PILA
Data desencolar(cola*);
Data primero(cola*);
bool es_vacia(cola *);
int cuantos(cola*);
bool anular(cola*);

#endif 


----------------------------------------------------------------------------------------------------------------------------

Lista ligada
lista_lig.h
#ifndef __LISTA_LIG_H__
#define __LISTA_LIG_H__
#include "Nodo.h"
#include <stdbool.h>

typedef struct Lista{
    Nodo *head;
    Nodo *tail;
    int num;
}Lista;

Lista *crear_lista();
void borrar_lista(Lista *l);
void insertar(Lista *l, Data d);
void eliminar(Lista *l, Data d);
Nodo *buscar(Lista *l, Data d);
void imprimir(Lista *l);

#endif

----------------------------------------------------------------------------------------------------------------------------

Lista Doblemente Ligada (Doblemente Enlazada)
ListaDE.h
#ifndef __LISTA_DE_H__
#define __LISTA_DE_H__
#include "Nodo.h"
#include <stdbool.h>

typedef struct Lista{
    Nodo *head;
    Nodo *tail;
    int num;
}ListaDE;

ListaDE *crear_lista();
void borrar_lista(ListaDE *l);

void insertar_head(ListaDE *l, Data d);
void insertar_tail(ListaDE *l, Data d);

void eliminar_head(ListaDE *l);
void eliminar_tail(ListaDE *l);


Nodo *buscar(ListaDE *l, Data d);
void imprimir(ListaDE *l);

#endif

----------------------------------------------------------------------------------------------------------------------------

pila.h
#ifndef __PILA_H__
#define __PILA_H__
#include "Nodo.h"

struct _pila
{
    Nodo* cima; //head o tail
    Nodo* fondo; //head o tail
    int lon;//Longitud y numero de datos de la pila
};

typedef struct _pila pila;

pila* pila_vacia();
bool push(pila*,DATA);//RECIBE UN APUNTADOR A LA `PILA
DATA pop(pila*);
DATA top(pila*);
bool es_vacia(pila *);
int cuantos(pila*);
bool anular(pila*);


#endif 

----------------------------------------------------------------------------------------------------------------------------
OPERACIONES en .c |
------------------|


Nodo.c
#include "Nodo.h"
#include <stdlib.h>

/**
 * @brief CREAR NODO :
 * Es capaz de crear un nodo, un espacio para un elemento.
 * 
 * @param d 
 * @return Nodo* 
 */
Nodo *crear_nodo(Data d){
    Nodo *n = (Nodo*)malloc(sizeof(Nodo));
    n->dato = d;
    //elemento anterior a n
    n->ant = NULL;
    //elemento posterior a n
    n->sig = NULL;
    return n;
}

void borrar_nodo(Nodo *n){
    if(n->sig == NULL){
        free(n);
    }
}

void actualizar_nodo(Nodo *n, Data d){
    if(n != NULL){
        n->dato = d;
    }
}

----------------------------------------------------------------------------------------------------------------------------

Cola.c



----------------------------------------------------------------------------------------------------------------------------

Lista_lig.c
#include "lista_lig.h"
#include <stdio.h>
#include <stdlib.h>

Lista *crear_lista(){
    Lista *l = (Lista*)malloc(sizeof(Lista));
    l->head = NULL;
    l->tail = NULL;
    l->num = 0;
    return l;
}

void borrar_lista(Lista *l){
    Nodo *tmp = l->head;
    while(l->num != 0){
        l->head = l->head->sig;
        free(tmp); 
        tmp = l->head;
        l->num--;
    }
    free(l);
}

void insertar(Lista *l, Data d){
    // - DEBE DE SER INSERTADO AL INICIO DE LA LISTA
    // - head (como apuntador) debe apuntar al nodo que se quiere insertar.
    Nodo* newnodo = crear_nodo(d);
    newnodo->sig = l->head;
    l->head = newnodo;
    l->num++;
    return;
}

void eliminar(Lista *l, Data d){
    Nodo *tmp = l->head;
    Nodo *ant = NULL;
    while(tmp != NULL){
        if(tmp->dato==d){
            //Cuando se borra el primer nodo ant = NULL
            ant = NULL;
            return;
        }
        ant = tmp;
        tmp = tmp->sig;
    }
    return;
}

Nodo *buscar(Lista *l, Data d){
    Nodo *tmp = l->head;
    while(tmp != NULL){
        if(tmp->dato==d) return tmp;
        tmp = tmp->sig;
    }
    return NULL;
}

void imprimir(Lista *l){
    if(l != NULL){
        printf("[ ");
        for(Nodo *tmp=l->head; tmp!=NULL; tmp =tmp->sig){
            printf("%d ", tmp->dato);
        }
        printf("]\n");
    }else{
        printf("NO HAY LISTA QUE MOSTRAR\n");
    }
}

----------------------------------------------------------------------------------------------------------------------------

ListaDE.c
#include "ListaDE.h"
#include "Nodo.h"
#include <stdio.h>
#include <stdlib.h>

//NO HAY MODIFICACIONES POR EL USO QUE SE LE DA
ListaDE *crear_lista(){
    ListaDE *l = (ListaDE*)malloc(sizeof(ListaDE));
    l->head = NULL;
    l->tail = NULL;
    l->num = 0;
    return l;
}

//NO HAY MODIFICACIONES POR EL USO QUE SE LE DA
void borrar_lista(ListaDE *l){
    Nodo *tmp = l->head;
    while(l->head != 0){
        l->head = l->head->sig;
        free(tmp); 
        tmp = l->head;
        l->num--;
    }
    free(l);
}

//Evaluamos si se tiene una lista previa; si no, esta funcion actua
void insertar_head(ListaDE *l, Data d){
    Nodo* newnodo = crear_nodo(d);
    newnodo->sig = l->head;
    l->head = newnodo;
    return;
}

void insertar_tail(ListaDE *l, Data d){
    Nodo* newnodo = crear_nodo(d);
    newnodo = l->tail;
    l->tail = newnodo;
    return;
}


void eliminar_head(ListaDE *l){
    Nodo *tmp = l->head;
    if(tmp != NULL) {
        l->head = l->head->sig;
        borrar_nodo(tmp);
    }
}

void eliminar_tail(ListaDE *l){
    Nodo *tmp = l->head->sig;
    if(tmp != NULL){
        l->head->sig = l->head->sig->sig;
        borrar_nodo(tmp);
    }
}

Nodo *buscar(ListaDE *l, Data d){
    Nodo *tmp = l->head;
    while(tmp != NULL){
        if(tmp->dato==d) return tmp;
        tmp = tmp->sig;
    }
    return NULL;
}

void imprimir(ListaDE *l){
    if(l != NULL){
        printf("[ ");
        for(Nodo *tmp=l->head; tmp!=NULL; tmp =tmp->sig){
            printf("%d ", tmp->dato);
        }
        printf("]\n");
    }else{
        printf("NO HAY LISTA QUE MOSTRAR\n");
    }
}

----------------------------------------------------------------------------------------------------------------------------

Pila.c





