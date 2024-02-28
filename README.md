#include<stdio.h>
#include<stdlib.h>
struct node
{
	char ssn[10],name[20],dept[30],desig[30];
	float sal;
	long int ph;
	struct node *llink,*rlink;
};
typedef struct node*NODE;
NODE getnode()
{
	NODE x;
	x=(NODE)malloc(sizeof(struct node));
	if(x==NULL)
	{
	printf("Memory is not allocated");
	exit(0);
	}
	return x;
}
NODE ins_front(NODE f)
{
	NODE t;
	t=getnode();
	t->rlink=t->llink=NULL;
	printf("Enter SSN,Name,dept,desig,salary,phone of the emp\n");
	scanf("%s %s %s %s %f %ld",t->ssn,t->name,t->dept,t->desig,&(t->sal),&(t->ph));	
	if(f==NULL)
	{
		return t;
	}
	else
	{
		t->rlink=f;
		f->llink=t;
		return t;
	}
}
NODE ins_rear(NODE f)
{
	NODE cur,t;
	t=getnode();
	t->rlink=t->llink=NULL;
	if(f==NULL)
	{
		return t;
	}
	printf("Enter SSN,Name,dept,desig,salary,phone of the emp\n");
	scanf("%s%s%s%s%f%ld",t->ssn,t->name,t->dept,t->desig,&(t->sal),&(t->ph));
	while(cur->rlink!=NULL)
	{
		cur=cur->rlink;
	}
	cur->rlink=t;
	t->llink=cur;
	return f;
}
NODE create(NODE f)
{
	int n,i;
	printf("Enter value for n\n");
	scanf("%d",&n);
	for(i=0;i<n;i++)
	{
		f=ins_front(f);
	}
	return f;
	}
void status(NODE f)
{
	int cnt=0;
	NODE cur;
	cur=f;
	while(cur!=NULL)
	{
		cur=cur->rlink;
		cnt++;
	}
	printf("Number of nodes in SLL is %d\n",cnt);
	
}

NODE del_front(NODE f)
{
	NODE t;
	if(f==NULL)
	{
		printf("DLL is empty\n");
		return f;
	}
	if(f->rlink==NULL)
	{
		printf("Information to be deleted\n");
		printf("%s\t%s\t%s\t%s\t%f\t%ld\n",f->ssn,f->name,f->dept,f->desig,f->sal,f->ph);
		free(f);
		return NULL;
	}
	t=f->rlink;
	t->llink=NULL;
	printf("Information to be deleted\n");
	printf("%s\t%s\t%s\t%s\t%f\t%ld\n",f->ssn,f->name,f->dept,f->desig,f->sal,f->ph);
	free(f);
	return t;
}
NODE del_rear(NODE f)
{
	NODE prev,cur;
	if(f==NULL)
	{
	printf("NO elements in DLL");
	return f;
	}
	if(f->rlink==NULL)
	{	
	printf("Information to be deleted\n");
	printf("%s\t%s\t%s\t%s\t%f\t%ld\n",f->ssn,f->name,f->dept,f->desig,f->sal,f->ph);
	free(f);
	return NULL;
	}
	prev=NULL;
	cur=f;
	while(cur->rlink!=NULL)
	{	
	prev=cur;
	cur=cur->rlink;
	}
	prev->rlink=NULL;
	printf("Information to be deleted\n");
	printf("%s\t%s\t%s\t%s\t%f\t%ld\n",cur->ssn,cur->name,cur->dept,cur->desig,cur->sal,cur->ph);
	free(cur);
	return f;
}
NODE display(NODE f)
{
	NODE cur;
	if(f==NULL)
	{
	printf("No elements in DLL");
	return f;
	}
	cur=f;
	printf("Elements of DLL");
	while(cur!=NULL)
	{
	printf("%s\t%s\t%s\t%s\t%f\t%ld\n",cur->ssn,cur->name,cur->dept,cur->desig,cur->sal,cur->ph);
	cur=cur->rlink;
	}
}
int main()
{
	NODE first=NULL;
	int ch;
	while(1)
	{
				printf("1.create\n2.ins_front\n3. ins_rear\n4.del_front\n5.del_rear\n6.status\n.display\n8.exit\n");
		scanf("%d",&ch);
		switch(ch)
		{
		case 1:first=create(first);
		break;
		case 2:
		first=ins_front(first);
		break;
		case 3:first=ins_rear(first);
		break;
		case 4:
		first=del_front(first);
		break;
		case 5:
		first=del_rear(first);
		break;
		case 6:
		status(first);
		break;
		case 7:
		first=display(first);
		break;
		default:exit(0);
		}
	}
}
