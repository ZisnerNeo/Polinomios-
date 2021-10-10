# Polinomios-
Son evaluados y derivados (variable x solamente)
/*
 Trabajo:  Programa Evaluador y Derivador de Polinomios con Listas Simples UASLP © 2021-2022/I.
 Autor:    CISNEROS LOPEZ ROBERTO NOE.
 Profesor: Dr. CASTILLO BARRERA FRANCISCO EDGAR.
 FECHA:    08/Octubre/2021.
*/
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <conio.h>

typedef struct nodo{
	int coeficiente;
	int exponente;
	int coeficienteDerivado;
	int exponenteDerivado;
	struct nodo *sig;
}TPolinomio;

void presentacion(void);
int pideExponente(int exponente);
int pideCoeficiente(int coeficiente);
TPolinomio *creaNodo(int coeficiente,int exponente);
int insertaPolinomio(TPolinomio **Cab, int coeficiente,int exponente);
int imprimirlista(TPolinomio *Cab);
int derivarPolinomio(TPolinomio *Cab);
int imprimirlistaDerivada(TPolinomio *Cab);
int eliminarlistaPolinomios(TPolinomio **Cab);
int evaluarPolinomio(TPolinomio **Cab);
int imprimirPolinomiosEvaluados(TPolinomio *Cab);
void eliminarlistaEnSalida(TPolinomio **Cab);
void despedida(void);   

int main()
{
  int coefi,exp,opcion;
  TPolinomio *Cab=NULL;
  presentacion();
  printf("Opciones:\n1- Ingresa la variable\n2- Imprimir lista\n3- Imprimir lista derivada\n4- Evaluar Polinomio\n5- Eliminar lista & limpiar la pantalla\n");
  printf("\nPresione 0 para salir...\n");
  do{system("color 3");
  	 printf("\n\t\tIntroduzca la opcion seleccionada:\n");
     printf("Opci%cn: ",162);scanf("%d",&opcion);
  switch(opcion){
  	
  	case 0: despedida();
  	 		eliminarlistaEnSalida(&Cab);
  	        break;
	case 1: system("color 2");	
			insertaPolinomio(&Cab,coefi,exp);
			printf("\n");
            break;
	case 2: system("color 5");
	        imprimirlista(Cab);
            printf("\n");    
			break; 
	case 3: system("color A");
	        imprimirlistaDerivada(Cab);
            printf("\n");  
            break;
    case 4: system("color 4");
	        evaluarPolinomio(&Cab);
            printf("\n");
			break; 
	case 5: system("color BD");
			eliminarlistaPolinomios(&Cab);
			printf("\n");  
			printf("Opciones:\n1- Ingresa la variable\n2- Imprimir lista\n3- Imprimir lista derivada\n4- Evaluar Polinomio\n5- Eliminar lista & limpiar la pantalla\n");
   			printf("\nPresione 0 para salir...\n"); 
			break;       
	default:system("color C");
	        printf("Porfavor, seleccione una opcion correcta\n");  
            printf("\n");
            getch();
	  }
 }while(opcion!=0);
}

int pideExponente(int exponente)
{   
	printf("Dame el exponente de la variable:\n");
	printf("Exponente: "); scanf("%d",&exponente);
	return exponente;
}

int pideCoeficiente(int coeficiente)
{
	printf("Dame el coeficiente de la variable:\n");
	printf("Coeficiente: "); scanf("%d",&coeficiente);
	return coeficiente;
}

TPolinomio *creaNodo(int coeficiente,int exponente)
{   
	TPolinomio *nuevo=NULL;
	nuevo=(TPolinomio*)malloc(sizeof(TPolinomio));
	if(nuevo!=NULL){
	  nuevo->coeficiente=pideCoeficiente(coeficiente);
	  nuevo->exponente=pideExponente(exponente);
      nuevo->coeficienteDerivado=NULL;
	  nuevo->exponenteDerivado=NULL;
	  nuevo->sig=NULL;
   } return nuevo;
}

int insertaPolinomio(TPolinomio **Cab, int coeficiente,int exponente)
{  int bandera = 0;
   TPolinomio *nuevo,*aux;
   nuevo = creaNodo(coeficiente,exponente);
   if(nuevo){
    if(*Cab == NULL ) 
       { *Cab = nuevo;
    }else{
     for(aux=*Cab;aux->sig!=NULL;aux=aux->sig);
        aux->sig=nuevo;
   }
} bandera++;
   return (bandera);
}

int imprimirlista(TPolinomio *Cab)
{
	int bandera=0;
	TPolinomio *aux=Cab;
	if(Cab){
		printf(" Polinomio:  ");
	while(aux!=NULL){
	if(aux->exponente==1){
	printf("+ %dx ",aux->coeficiente);
	    aux=aux->sig;
		bandera++;	
	}	
     if(aux->exponente==0){
      	printf("+ %d ",aux->coeficiente);
	    aux=aux->sig;
	    bandera++;
	 } else{
	 printf("+ %dx^%d ",aux->coeficiente,aux->exponente);
	    aux=aux->sig;
	    bandera++;
    }	
   }	
 }  return bandera;
    if(Cab==NULL)
	printf("No hay variables registradas\n");	
 
}


int imprimirlistaDerivada(TPolinomio *Cab)
{   
    int bandera=0;
	derivarPolinomio(Cab);
	TPolinomio *aux=Cab;
	if(Cab!=NULL){	printf(" Polinomio Derivado:  ");
	  	while(aux!=NULL){
     		if(aux->exponente==1 || aux->exponente==0){	
				printf(" ");
	 			aux=aux->sig;
	 			bandera++;	 
			}else{
          printf("+ %dx^%d ",aux->coeficienteDerivado,aux->exponenteDerivado);
	 	  aux=aux->sig;
 	 	  bandera++;	
	       }
				   }				
  } 
    if(Cab==NULL)
	printf("No hay variables derivadas registradas\n");	
	return bandera;
 }   			 
				
int derivarPolinomio(TPolinomio *Cab)
{   int bandera=0;
	TPolinomio *aux = Cab;
	if(Cab){
	while(aux!=NULL){
		 aux->coeficienteDerivado=aux->coeficiente*aux->exponente;
		 aux->exponenteDerivado=aux->exponente-1;
		 aux=aux->sig;
		 bandera++;
	} 
   }  return bandera;
}

int evaluarPolinomio(TPolinomio **Cab)
{   
    TPolinomio *aux=NULL;    
    int bandera=0,x;
    long sum=0,temp=0;
    printf("Dame el valor de la variable (x):  ");
	scanf("%d",&x);
	if(*Cab!=NULL){		
	 for(aux=*Cab;aux!=NULL;aux=aux->sig){
	  temp=(pow(x,aux->exponente))*aux->coeficiente;
	  sum=sum+temp;
	  bandera++;
	}
}	printf("\nEl valor evaluado del polinomio es:  %d\n",sum);
    return bandera;
}

int eliminarlistaPolinomios(TPolinomio **Cab)
{ 
    int bandera=0;
    TPolinomio *aux;
    aux=*Cab;  
    if(*Cab!=NULL){
	     do{
     			*Cab=aux->sig;
       			free (aux);
       			bandera++;
     		}while(*Cab=NULL);
   }if(*Cab==NULL){
  			printf("\n\tLa lista esta vacia ahora\n");
  			}system("pause");
   		 	 system("cls");
  	return bandera;
}

void eliminarlistaEnSalida(TPolinomio **Cab)
{ 
    TPolinomio *aux;
    aux=*Cab;  
    if(*Cab!=NULL){
	       	do{   
     			*Cab=aux->sig;
       			free (aux);
     		}while(*Cab=NULL);
 } 	exit(1);
}

void presentacion(void)
{   
    int i=0;
    system("color 5");
    printf("\n\n\n\n\tHola <3, pulsa una tecla para avazar!!!\n");
    getch();
	for(;i<1;i++){
	system("color 16");	
	printf("\n\n\t///////////////////////////////////////////////////////////\n\n");
	printf("\tBienvenido a mi trabajo evaluador y derivador de polinomios\n\tMi nombre es ROBERTO NOE CISNEROS LOPEZ ^U^\n\tEspero que disfrutes mi programa <3\t");
	printf("\n\n\t///////////////////////////////////////////////////////////\n\n");
	getch();
	system("cls");
	}
	system("color 3");
}

void despedida(void)
{   
    printf("\n\n\t//////////////////////////////////////////\n\n");
	printf("\tMuchisimas gracias por ver mi programa <3\n");
	printf("\tEspero haya sido de su agrado n.n");
    printf("\n\n\t//////////////////////////////////////////\n\n");
}
