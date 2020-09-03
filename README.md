# PigFarm
#include<stdlib.h>
#include<string>
#include<iostream>
#include<ctime>
#include<windows.h>
using namespace std;
static int I = 0;
static int i = 0;
typedef struct Pig{//猪
    int pigstynum;
    int num;
    string type;
    double weight;
    double time;
    bool black;
}pig;

typedef struct Pigsty{//猪圈
    int no;
    int pignum = 0;
    struct node *a;
}pigsty;


typedef struct Node//猪圈指针
{
    pigsty Data;
    struct Node *next;
}Lnode;

typedef struct node//猪指针
{
    pig data;
    struct node *next;
}lnode;

void Creat(Lnode *h,int n)//生成猪圈
{
    Lnode *p,*r;
    int j;
    r=h;
    for(j=0;j<n;j++)
    {
        p=(Lnode *)malloc(sizeof(Lnode));
        r->next=p;
        r->Data.no = I;
        I++;
        lnode *hh;
        hh=(lnode *)malloc(sizeof(lnode));
        hh->next=NULL;
        r->Data.a = hh;
        creat(hh, 10);
        r=p;
    }
    r->next=NULL;
}

void creat(lnode *h,int n)//生成猪槽
{
    lnode *p,*r;
    int j;
    r=h;
    for(j=0;j<n;j++)
    {
        p=(lnode *)malloc(sizeof(lnode));
        r->next=p;
        r=p;
    }
    r->next=NULL;
}

void random(pig u)//随机生成一个猪
{
    string tp;
    double weight;
    weight=rand() % 30;
    weight=weight+20.00;
    int tpnum;
    tpnum = rand() % 3;
    switch(tpnum){
        case 0:
            tp = "黑猪";
            break;
        case 1:
            tp = "小花猪";
            break;
        case 2:
            tp = "大花白猪";
            break;
        }; 
    if(tp=="黑猪") u.black = 1;
    u.type = tp;
    u.weight = weight;
}

void Input(Lnode *p)//放1猪进猪圈
{
    Lnode *r = p;
    pig u;
    random(u);
    for (int i = 0; i < 10;i++){
        for (; r != NULL; r = r->next)
        {
            if (r->Data.pignum != i)
                r = r->next;
            if (r->Data.a->data.black)
            {
                if (!u.black) r = r->next;
            };
            p->Data.a->data.weight = u.weight;
            p->Data.a->data.type = u.type;
            p->Data.pignum++;
        }
    }   
}

void output(Lnode *h)//输出
{
    Lnode *p;
    p=h->next;
    while(p!=NULL)
    {
        cout<<p->Data.no<<endl;
        p->Data.a = p->Data.a->next;
        while(p->Data.a!=NULL){
            cout << p->Data.a->data.num << p->Data.a->data.type << p->Data.a->data.weight << " ";
            p->Data.a = p->Data.a->next;
        }
        cout << endl;
        p=p->next;
    }
}




int main()
{
    Lnode *b;
    b=(Lnode *)malloc(sizeof(Lnode));
    b->next = NULL;
    Creat(b,100);
    output(b);
    return 0;
}
