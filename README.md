#include <iostream>
#include <cstdlib>
#include <string.h>
using namespace std;

struct node
{
    char label[30];
    int ch_count;
    struct node *child[30];
} *root;

class GT
{
public:
    void create_tree();
    void display(node *r1);

    GT( )
    {
        root = NULL;
    }
};

void GT::create_tree()
{
    int tchapters, i, j;
    root = new node();
    cout << "Enter Name of Book : ";
    cin >> root->label;
    cout << "Enter no. of Chapters in Book: ";
    cin >> tchapters;
    root->ch_count = tchapters;

    for (i = 0; i < tchapters; i++)
    {
        root->child[i] = new node;
        cout << "\nEnter Chapter " << i + 1 << " Name: ";
        cin >> root->child[i]->label;
        cout << "Enter no. of Sections in Chapter " << root->child[i]->label << ": ";
        cin >> root->child[i]->ch_count;

        for (j = 0; j < root->child[i]->ch_count; j++)
        {
            root->child[i]->child[j] = new node;
            cout << "\nEnter Section " << j + 1 << " name: ";
            cin >> root->child[i]->child[j]->label;
        }
    }
}

void GT::display(node *r1)
{
    int i, j;
    if (r1 != NULL)
    {
        cout << "\n-----Book-----\n";
        cout << "BOOK TITLE: " << r1->label;
        cout << "\n*** CHAPTERS ***" << endl;

        for (i = 0; i < r1->ch_count; i++)
        {
            cout << "\n" << i + 1 << ". " << r1->child[i]->label;

            for (j = 0; j < r1->child[i]->ch_count; j++)
            {
                cout << "\n\t" << i + 1 << "." << j + 1 << ". " << r1->child[i]->child[j]->label;
            }
        }
    }
}

int main()
{
    int choice;
    GT gt;
  
    while (1)
    {
        cout << "\n-----------------" << endl;  
        cout << "Book Tree Creation" << endl;
        cout << "-----------------" << endl;
        cout << "1.Create" << endl;
        cout << "2.Display" << endl;
        cout << "3.Quit" << endl;
        cout << "Enter your choice : ";
        cin >> choice;

        switch (choice)
        {
        case 1:
            gt.create_tree();
            break;
        case 2:
            gt.display(root);
            break;
        case 3:
            exit(1);
        default:
            cout << "\nWrong Choice!" << endl;
        }
    }
}

