# Remove-loop-LL
Detect and remove if a loop is present there in a linked list. Two pointers approach Floyd cycle detection used.
//Remove loop in a linked list
#include<iostream>
using namespace std;

struct Node{
	int data;
	Node* next;
	Node(int d){
		data=d;
		next=NULL;
	}	
};

void detectRemoveLoop(Node* head){
	Node* slow=head,*fast=head;
	while(fast!=NULL || fast->next!=NULL){
		slow=slow->next;
		fast=fast->next->next;
		if(slow==fast){
			break;
		}
	}
	if(slow!=fast){
		return;
	}
	slow=head;
	while(slow->next!=fast->next){
		slow=slow->next;
		fast=fast->next;
	}
	fast->next=NULL;
}

void printList(Node* head)
{
	if(head==NULL){
		return;
	}
	Node* curr=head;
	while(curr!=NULL){
		cout<<curr->data<<" ";
		curr=curr->next;
	}	
}

int main(){
	Node* head=new Node(15);
	head->next=new Node(10);
	head->next->next=new Node(12);
	head->next->next->next=new Node(20);
	head->next->next->next->next=head->next;
	detectRemoveLoop(head);
	printList(head);
	return 0;
}
