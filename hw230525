#include <stdio.h>
#include <stdlib.h>

#define FILENAME "product.bat"

struct product{
    int id;
    char name[20];
    float price;
    int stock;
};

void addproduct();
void updateproduct();
void showproduct();
void deleteproduct();
int menu();

int main(void){
menu();
return 0;
}

int menu(){

    while(1){
    int choice;

    printf("\n******ISLEM LISTESI******\n");
    printf("1-Urun Ekleme\n");
    printf("2-Urun Guncelleme\n");
    printf("3-Urun Goster\n");
    printf("4-Urun Silme\n");
    printf("5-Cikis");
    printf("Secim yapiniz: ");
    scanf("%d",&choice);
    switch (choice){

        case 1:
        addproduct();
        break;

        case 2:
        updateproduct();
        break;

        case 3:
        showproduct();
        break;

        case 4:
        deleteproduct();
        break;

        case 5:
        printf("Basariyla cikis yapildi!");
        return 0;
        
        default:
        printf("Gecersiz Secim!\n");
        break;
        }
    }
}



void addproduct(){
    struct product p;
    FILE* file=fopen(FILENAME,"ab");

    printf("Urun ID: ");
    scanf("%d",&p.id);
    printf("Urun Adi: ");
    scanf("%s",p.name);
    printf("Urun Fiyati: ");
    scanf("%f",&p.price);
    printf("Urun Miktari: ");
    scanf("%d",&p.stock);


    fwrite(&p,sizeof(struct product),1,file);
    fclose(file);
    printf("Urun basariyla eklendi.\n");
}



void updateproduct(){
    struct product p;
    int id,newstock=0;

    FILE* file=fopen(FILENAME,"rb+");

    printf("Guncellemek istenilen urunun ID kodunu giriniz: \n");
    scanf("%d",&id);

    fseek(file,(id-1)*sizeof(struct product),SEEK_SET);
    fread(&p,sizeof(struct product),1,file);

    printf("Yeni stok miktari: \n");
    scanf("%d", &newstock);
    p.stock=newstock;

    fseek(file,(id-1)*sizeof(struct product),SEEK_CUR);
    fwrite(&p,sizeof(struct product),1,file);
    fclose(file);
    printf("Dosya basariyla guncellendi!\n");

}

void showproduct() {
    struct product p;
    FILE* file = fopen(FILENAME, "rb");

    if (file == NULL) {
        printf("Dosya bulunamadi.\n");
    }

    printf("\n-----URUN LISTESI-----\n");
    while (fread(&p, sizeof(struct product), 1, file) == 1) {
        printf("ID: %d\n", p.id);
        printf("Ad: %s\n", p.name);
        printf("Fiyat: %.2f\n", p.price);
        printf("Stok: %d\n", p.stock);
        printf("----------------------\n");
    }
    fclose(file);
}

void deleteproduct(){
    struct product p;
    int delete_id;
    int found = 0;

    FILE* file = fopen(FILENAME, "rb");
    FILE* temp = fopen("temp.dat", "wb");

    if (file == NULL || temp == NULL) {
        printf("Dosya acilamadi.\n");
        return;
    }

    printf("Silmek istediginiz urunun ID'sini giriniz: ");
    scanf("%d", &delete_id);

    while (fread(&p, sizeof(struct product), 1, file) == 1) {
        if (p.id != delete_id) {
            fwrite(&p, sizeof(struct product), 1, temp);
        } else {
            found = 1;
        }
    }

    fclose(file);
    fclose(temp);

    if (found) {
        remove(FILENAME);              
        rename("temp.dat", FILENAME);  
        printf("Urun basariyla silindi.\n");
    } else {
        remove("temp.dat");
        printf("ID bulunamadi. Silme islemi basarisiz.\n");
    }

}
