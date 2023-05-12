# 1220505060.4.soru
kuyruk yapısınna eleman eklme,elman silme
#include <stdio.h>
#include <stdlib.h>

// Kuyruk elemanının yapısı
struct node {
    int data;
    struct node* next;
};

// Kuyruk yapısı
struct queue {
    struct node* front;
    struct node* rear;
};

// Yeni bir kuyruk oluşturma fonksiyonu
struct queue* createQueue() {
    struct queue* q = (struct queue*)malloc(sizeof(struct queue));
    q->front = q->rear = NULL;
    return q;
}

// Yeni bir eleman eklemek için fonksiyon
void enqueue(struct queue* q, int x) {
    struct node* temp = (struct node*)malloc(sizeof(struct node));
    temp->data = x;
    temp->next = NULL;

    if (q->rear == NULL) {
        q->front = q->rear = temp;
        return;
    }

    q->rear->next = temp;
    q->rear = temp;
}

// Bir elemanı silmek için fonksiyon
void dequeue(struct queue* q) {
    if (q->front == NULL) {
        printf("Kuyruk bos\n");
        return;
    }

    struct node* temp = q->front;
    q->front = q->front->next;

    if (q->front == NULL) {
        q->rear = NULL;
    }

    free(temp);
}

// Kuyruktaki tüm elemanları yazdırmak için fonksiyon
void display(struct queue* q) {
    if (q->front == NULL) {
        printf("Kuyruk bos\n");
        return;
    }

    struct node* temp = q->front;
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}

// Ana fonksiyon
int main() {
    struct queue* q = createQueue();
    int secim, eleman;

    do {  //Kuyruğa eleman ekle: Kullanıcı, eklenecek bir elemanın değerine girmelidir. Bu eleman kuyruğun sonuna eklenir.bunun için case lerden bırı seçilmelifir
        printf("\n\n1-Ekle\n2-Sil\n3-Goruntule\n4-Cikis\nSecim yapiniz: ");
        scanf("%d", &secim);

        switch (secim) {
            case 1:
                printf("Eklemek istediginiz elemani girin: ");//eleman eklemek için 1 basılmalıdır.
                scanf("%d", &eleman);
                enqueue(q, eleman);
                break;
            case 2:
                dequeue(q);
                break;
            case 3:
                printf("Kuyruk: ");
                display(q);
                break;
            case 4:
                printf("Programdan cikiliyor.\n");//programdan çıkmakk için 4 tıklanmalıdır.
                break;
            default:
                printf("Gecersiz secim.\n");
        }

    } while (secim != 4);//secim 4 e eşt dehıl se dongo devam etsınnn hocammmmm:)))

    return 0;
}
