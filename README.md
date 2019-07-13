# linkedlist

We are bumping into a basic "feature" of the C language that changes to local parameters
are never reflected back in the caller's memory. This is a traditional tricky area of C
programming. We will present the traditional "reference parameter" solution to this
problem, but you may want to consult another C resource for further information. (See
Pointers and Memory (http://cslibrary.stanford.edu/102/) for a detailed explanation of
reference parameters in C and C++.)
We need Push() to be able to change some of the caller's memory — namely the head
variable. The traditional method to allow a function to change its caller's memory is to
pass a pointer to the caller's memory instead of a copy. So in C, to change an int in the
caller, pass a int* instead. To change a struct fraction, pass a struct
fraction* intead. To change an X, pass an X*. So in this case, the value we want to
change is struct node*, so we pass a struct node** instead. The two stars
(**) are a little scary, but really it's just a straight application of the rule. It just happens
that the value we want to change already has one star (*), so the parameter to change it
has two (**). Or put another way: the type of the head pointer is "pointer to a struct
node." In order to change that pointer, we need to pass a pointer to it, which will be a
"pointer to a pointer to a struct node".
Instead of defining WrongPush(struct node* head, int data); we define
Push(struct node** headRef, int data);. The first form passes a copy of
the head pointer. The second, correct form passes a pointer to the head pointer. The rule
is: to modify caller memory, pass a pointer to that memory. The parameter has the word
"ref" in it as a reminder that this is a "reference" (struct node**) pointer to the
head pointer instead of an ordinary (struct node*) copy of the head pointer.
