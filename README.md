# Newton-Raphson
Repositorio Metodo Newton Raphson
#include <iostream>
#include <math.h>

using namespace std;
float Funcion(char*,int);
float Funcion_Der(char*,int);
float numero(char*,int);
int main()
{
    char Fun[50];
    float Aprox[180],Camb[180],Raiz[180];
    int IndCamb=0;
    cout<<"Escriba el polinomio de forma que si quiere ingresar 'x^2-x-6' debe ingresar"<<endl;
    cout<<"+1X**2-1X**1-6X**0 entre comillas, NO olvidar el primer signo y X mayuscula"<<endl<<endl;
    cout<<"ingrese su polinomio : ";
    cin.getline(Fun,50);
    for(int i=-90;i<90;i++){
        Aprox[i]=Funcion(Fun,i);
    }
    for(int k=-90;k<89;k++){


        if(Aprox[k]<0){
            if(Aprox[k+1]>0){
                Camb[IndCamb]=k;
                IndCamb++;
            }
        }
        if(Aprox[k]>0){
            if(Aprox[k+1]<0){
                Camb[IndCamb]=k;
                IndCamb++;
            }
        }
        if(Aprox[k]==0){
        cout<< "RAIZ = "<<k<<endl;
        }
    }
    int whl=0;
    float x0,x1,Tolerancia=0.001,Error=10;
    while(whl<IndCamb){
        x0=Camb[whl];
        Error=10;
        while(Error>Tolerancia){
            x1=x0-Funcion(Fun,x0)/Funcion_Der(Fun,x0);
            Raiz[whl]=x1;
            x0=x1;
            Error= fabs(x1-x0);

        }
        cout<< "RAIZ = "<< Raiz[whl]<<endl;
        whl++;
    }

    return 0;
}

float Funcion(char Fun[],int X){

    int i=1,k=0,numer=0;
    float h,resp[50],exp,aux,Xval;
    while(Fun[i]!='\0'){
        if(Fun[i]=='-'){
            i++;
            resp[k]=-1*numero(Fun,i);
        }
        if(Fun[i]=='+'){
            i++;
            resp[k]=numero(Fun,i);
        }
        if(Fun[i]=='*'){
            if(Fun[i+1]=='*'){
                aux=i+2;
                exp=numero(Fun,aux);
                Xval= pow(X,exp);
                numer=resp[k]*Xval+numer;
                k++;
            }
        }

    i++;
    }
    return numer;

}

float Funcion_Der(char Fun[],int X){

        int i=1,k=0,numer=0;
    float h,resp[50],exp,aux,Xval;
    while(Fun[i]!='\0'){
        if(Fun[i]=='-'){
            i++;
            resp[k]=-1*numero(Fun,i);
        }
        if(Fun[i]=='+'){
            i++;
            resp[k]=numero(Fun,i);
        }
        if(Fun[i]=='*'){
            if(Fun[i+1]=='*'){
                aux=i+2;
                exp=numero(Fun,aux)-1;
                Xval= pow(X,exp);
                resp[k]=resp[k]*(exp+1);
                numer=resp[k]*Xval+numer;
                k++;
            }
        }

    i++;
    }
    return numer;

}


float numero(char Fun[],int i){
    float resp[50],num;
    if((Fun[i]+0>47)and(Fun[i]+0<58)){
    resp[0]=Fun[i]-48;
        while((Fun[i+1]+0!=88)and(Fun[i+1]+0!=43)and(Fun[i+1]+0!=45)and(Fun[i+1]+0!=34)){
            resp[0]=resp[0]*10+(Fun[i+1]-48);
            i++;
        }
    }
    return num=resp[0];
}
