# sistema-academia
programa de gerenciamento e controle de alunos
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <conio.h>
#include <string.h>
#include <locale.h>


struct cliente{

    char nome[70],data_nasc[14],endereco[50],cep[10],rg[11],cpf[11];
};

struct atividade{
    char tipo[15],codigo[3],dias[20],horario[5],instrutor[20];
};

struct matricula{

    char nome[70],cpf[11];
    char tipo[15],codigo[3],dias[20],horario[5];
    int at;

};

typedef struct cliente aluno;
typedef struct atividade exercicio;
typedef struct matricula mat;



aluno fun_a;
exercicio fun_e;
mat fun_m;


FILE * bd_al;
FILE * bd_ex;
FILE * bd_mat;

 int op3=0;
     int op4=0;

void main(){
     setlocale(LC_ALL,"portuguese");
  int opcao=-1;
  int count =0;

   while(opcao != 6){
        system("cls");
     printf("                      \n\t 0 PARA CADASTRAR\n");
     printf("                      \n\t 1 PARA LISTAR ALUNOS\n");
     printf("                      \n\t 2 PARA CADASTRAR ATIVIDADE\n");
     printf("                      \n\t 3 PARA MATRICULAR ALUNO EM ATIVIDADE\n");
     printf("                      \n\t 4 LISTAR MATRICULADOS\n");
     printf("                      \n\t 5 EXCLUIR CADASTRO\n");
     printf("                      \n\t 6 SAIR             \n\n");
     printf("                      \n\t ESCOLHA A OPÇÃO:");
     scanf("%d", &opcao);

     switch(opcao){

   case 0: system("cls");
//setbuf(stdin,NULL);
    int opp;
        do{
    bd_al = fopen("cliente.txt","a+b");
    if (bd_al == NULL){
    printf("Um erro ocorreu ao tentar abrir o arquivo `cliente.txt'.\n");
    }else{
    system("cls");
    //printf("arquivo aberto com sucesso");
    printf("\nCADASTRO DE ALUNO\n");

    printf("NOME:");
    fflush(stdin);
    gets(fun_a.nome);
    printf("DATA DE NASCIMENTO:");
    fflush(stdin);
    gets(fun_a.data_nasc);
    printf("ENDEREÇO:");
    fflush(stdin);
    gets(fun_a.endereco);
    printf("CEP:");
    fflush(stdin);
    gets(fun_a.cep);
    printf("RG:");
    fflush(stdin);
    gets(fun_a.rg);
    printf("CPF:");
    fflush(stdin);
    gets(fun_a.cpf);

    fwrite(&fun_a,sizeof(aluno),1,bd_al);
    fclose(bd_al);
    system("pause");
    system("cls");

    printf("DESEJA CADASTRAR MAIS CLIENTES ? 1)CADASTRAR 2)SAIR\n");
    scanf("%d",&opp);

    }

    }while(opp!=2);
     break;





   case 1:system("cls");
  // setbuf(stdin,NULL);

      bd_al=fopen("cliente.txt","r+b");

    system("cls");
    while(fread(&fun_a,sizeof(aluno),1,bd_al)==1){

//while( fread(&func,sizeof(aluno),1,bd)==1){

    printf("\nNOME:%s\n", fun_a.nome);
    printf("DATA DE NASCIMENTO:%s\n", fun_a.data_nasc);
    printf("ENDEREÇO:%s\n", fun_a.endereco);
    printf("CEP:%s\n", fun_a.cep);
    printf("RG:%s\n", fun_a.rg);
    printf("CPF:%s\n", fun_a.cpf);
    system("pause");

    printf("-------------------------------\n");

    }
    fclose(bd_al);




        break;


        case 2: system("cls");
        setbuf(stdin,NULL);

        int op2;
        bd_ex=fopen("exercicio.txt","a+b");
   do{
        printf("ATIVIDADE:");
    fflush(stdin);
    gets(fun_e.tipo);
    printf("CÓDIGO:");
    fflush(stdin);
    gets(fun_e.codigo);
    printf("DIAS OFERTADOS:");
    fflush(stdin);
    gets(fun_e.dias);
    printf("HORÁRIO:");
    fflush(stdin);
    gets(fun_e.horario);
    printf("INSTRUTOR:");
    fflush(stdin);
    gets(fun_e.instrutor);

    fwrite(&fun_e,sizeof(exercicio),1,bd_ex);
    fclose(bd_ex);
    system("pause");
    system("cls");
    printf("DESEJA CADASTRAR MAIS ATIVIDADES ? 1)CADASTRAR 2)SAIR");
    scanf("%d",&op2);

}while(op2!=2);


     break;




     case 3:system("cls");

      int opp2;
     char cpf[11];
     char cod[3];

     int posicionar_al=0;
     int posicionar_ex=0;
     int achou_al=0;
     int achou_ex=0;


     fflush(stdin);
     printf("Digite o cpf: ");
     gets(cpf);
     fflush(stdin);
     printf("Digite o código da atividade");
     gets(cod);

     bd_al=fopen("cliente.txt","r+b");
     bd_ex=fopen("exercicio.txt","r+b");
     bd_mat=fopen("matricula.txt","a+b");
     system("cls");

     op3=-1;
     op4=-1;
     while(fread(&fun_a,sizeof(aluno),1,bd_al)==1 && op3!=0){
           if(strcmp(cpf,fun_a.cpf)==0){
            while(fread(&fun_e,sizeof(exercicio),1,bd_ex)==1 && op4!=0){
           if(strcmp(cod,fun_e.codigo)==0){



    printf("Nome:%s\n", fun_a.nome);
    printf("Atividade:%s\n", fun_e.tipo);
    printf("Dias ofertados:%s\n", fun_e.dias);
    printf("Horário:%s\n", fun_e.horario);



            printf(" Matricular 1)-sim 2)-não\n\n");
            scanf("%d",&opp2);

           if(opp2==1){
                   fun_m.at=1;
               strcpy(fun_m.nome,fun_a.nome);
               strcpy(fun_m.cpf,fun_a.cpf);

                strcpy(fun_m.tipo,fun_e.tipo);
                strcpy(fun_m.codigo,fun_e.codigo);
                strcpy(fun_m.dias,fun_e.dias);
                strcpy(fun_m.horario,fun_e.horario);








            fwrite(&fun_m,sizeof(mat),1,bd_mat);
                fclose(bd_mat);

             fseek(bd_ex,posicionar_ex,SEEK_SET);
      achou_ex=fwrite(&fun_e,sizeof(exercicio),1,bd_ex)==sizeof(exercicio);


           }
     if(opp2==2){
        break;
     }
             }
             posicionar_ex=posicionar_ex+sizeof(exercicio);
    fseek(bd_ex,posicionar_ex,SEEK_SET);
           }
           op4=-1;
fclose(bd_ex);

     }
      posicionar_al=posicionar_al+sizeof(aluno);
    fseek(bd_al,posicionar_al,SEEK_SET);

   }

    op3=-1;
fclose(bd_al);
break;


case 4: system("cls");
setbuf(stdin,NULL);

//listar a situação das matriculas
  bd_mat=fopen("matricula.txt","r+b");
  while(fread(&fun_m,sizeof(mat),1,bd_mat)==1){
        if(fun_m.at!=0){

    printf("Nome:%s\n", fun_m.nome);
    printf("Atividade:%s\n", fun_m.tipo);
    printf("Dias ofertados:%s\n", fun_m.dias);
    printf("Horário:%s\n", fun_m.horario);
        }



  }
system("pause");
  fclose(bd_mat);
  break;



case 5: system("cls");
setbuf(stdin,NULL);

setlocale(LC_ALL,"portuguese");
int psm=0;
int acm=0;
int op8=0;
char cpf_[11];
int g3;
setbuf(stdin,NULL);
printf("Digite o CPF a ser buscado: ");
gets(cpf_);
char nulo[10]=(" ");
system("cls");
bd_mat=fopen("matricula.txt","r+b");
op8=-1;
while(fread(&fun_a,sizeof(mat),1,bd_mat)==1 && op8!=0){
        if( strcmp(cpf_,fun_m.cpf)==0){


    printf("        Nome:%s\n", fun_m.nome);
    printf("        Atividade:%s\n", fun_m.tipo);
    printf("        Dias ofertados:%s\n", fun_m.dias);
    printf("        Horário:%s\n", fun_m.horario);



     printf("       Deseja realizar a exclusão dessa matrícula?\n");
    printf("        1)-sim\n");
    printf("        2)-não\n");
     scanf("%d",&g3);


      if(g3==1){

            fun_m.at=0;
            strcpy(fun_m.nome,nulo);
            strcpy(fun_m.tipo,nulo);
            strcpy(fun_m.dias,nulo);
            strcpy(fun_m.horario,nulo);

         fseek(bd_mat,psm,SEEK_SET);
      acm=fwrite(&fun_m,sizeof(mat),1,bd_mat)==sizeof(mat);

         break;




        }
        if(g3==2){
            break;

        }
        }
}
         psm=psm+sizeof(mat);
    fseek(bd_mat,psm,SEEK_SET);



    op8=-1;
fclose(bd_mat);


break;
    }









}
    }


