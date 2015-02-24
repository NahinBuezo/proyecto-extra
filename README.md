//# proyecto-extra
#include <iostream>
#include <cstring>
#include <cstdlib>
#include <vector>
#include <iomanip>
#include <ctime>
using namespace std;
void desordenar(char[], int);
int main(int argc, char*argv[]){
    bool terminar=false;
	int ca,cb;
	vector<char*>listo;
	cout<<"Ingrese el numero de palabras de la columna a"<<endl;
	cin>>ca;
	cb=ca;
    char c2[cb][25];
	char c1[ca][25];
	char referencia[ca*2][25];
    int selec,selec2;
    int posi;
    int errores=0;
    int correctos=0;
    int contador=0;
    int con=0;
    int con2=0;
  
	cout<<"Ingreso de palabras de columna A"<<endl;
	for(int i=0; i<ca; i++){
		char p1[25];
        cout<<"Ingrese palabra"<<i<<endl;
        cin>>p1;
        for(int w=0;w<25; w++){
        	c1[i][w]=p1[w];
        }
	}

	cout<<"Ingreso de palabras de columna B"<<endl;
	for(int i=0; i<cb; i++){
		char p2[25];
        cout<<"Ingrese palabra"<<i<<endl;
         cin>>p2;
        for(int w=0; w<25; w++){
        	c2[i][w]=p2[w];
        }
	}
	  
  
   
    cout<<"Es momento de emparejar las respuestas, debe seleccionar una opcion de la columna A y luego una de la conlumna B"<<endl;
    
    for(int i=0; i<ca*2; i++){
    	char pa[25];
    	char pa2[25];
 
    	if(i%2==0){
    	   for(int y=0; y<25; y++){
              pa[y]=c1[con][y];
    	   }
    	   con++;
    	
           for(int y=0; y<25; y++){
             referencia[i][y]=pa[y];
    	    }
    	    cout<<"Ingrese el numero de la posicion en la clomuna b, la cual corresponde a: "<<pa<<endl;
    	    cin>>posi;
         
    	    for(int y=0; y<25; y++){
              pa2[y]=c2[posi][y];
    	    }
	    	for(int y=0; y<25; y++){
	          referencia[i+1][y]=pa2[y];
	    	}
    	}
    	
    }//fin de crear la tabla de referencia

   
   //desordenando la columna a
	bool pos[ca];
	char columna[ca][25];
	
	srand(time(0));
	int index;
	for(int i=0; i<cb; i++){
		pos[i]=false;
	}

  
    for(int i=0; i<cb;i++){
        do{
        	index=rand()%cb;
        }while(pos[index]);
        
        for(int j=0; j<25; j++){
        	columna[i][j]=c1[index][j];
        }
        pos[index]=true;
    }
   

  //desordenando la columna b
    bool pos2[cb];
	char columna2[cb][25];
	
	
	int index2=0;
	for(int i=0; i<cb; i++){
		pos2[i]=false;
	}
  
    for(int i=0; i<cb;i++){
        do{
        	index2=rand()%cb;
        }while(pos2[index2]);
        
        for(int j=0; j<25; j++){
        	columna2[i][j]=c2[index2][j];
        }
        pos2[index2]=true;
    }
    contador=0;
    while(terminar==false){
        char wa[25];
        char wb[25];
        cout<<"  Columna A"<<setw(6)<<"Columna B"<<endl;

	    for(int i=0; i<cb ;i++){
	    	char word[25];
	    	char word2[25];
	    	for(int j=0; j<25; j++){
	    		word[j]=columna[i][j];
	    		word2[j]=columna2[i][j];
	    	} 
	    	
	    	cout<<i<<"."<<word<<setw(6)<<i<<"."<<word2<<endl;
	    	
	    }
	    cout<<"Seleccione posicion de columna A y luego de la columna B"<<endl;
	    cin>>selec>>selec2;
        for(int i=0; i<25; i++){
              wa[i]=columna[selec][i];
              wb[i]=columna2[selec2][i];
        }
        for(int j=0; j<cb*2;j++){
        	char mo[25];
        	char mo2[25];
        	for(int g=0; g<25; g++){	
        	   mo[g]=referencia[j][g];  	
        	}
        	if(strcmp(wa,mo)==0){
                for(int g=0; g<25; g++){
        	       mo2[g]=referencia[j+1][g];
        	    }
        		if(strcmp(wb,mo2)==0){
        			correctos++;
        			contador++;
        		}else{
        			contador++;
        			errores++;
        		}
        	}
        }
        if(contador==cb){
        	terminar=true;
        	cout<<"Termino el ejercio"<<endl;
        	cout<<"NUMERO DE ACIERTOS: "<<correctos<<endl;
        	cout<<"NUMERO DE ERRORES: "<<errores<<endl;
        	
        }
    }

    return 0;
}
