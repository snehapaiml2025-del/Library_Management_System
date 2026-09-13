#include <iostream>
#include <vector>
#include <string>
using namespace std;

class Book
{
public:
    int id;
    string title;
    string author;
    bool issued;

    Book(int i, string t, string a)
    {
        id = i;
        title = t;
        author = a;
        issued = false;
    }
};

class Library
{
private:
    vector<Book> books;

public:

    void addBook()
    {
        int id;
        string title, author;

        cout << "\nEnter Book ID: ";
        cin >> id;
        cin.ignore();

        cout << "Enter Book Title: ";
        getline(cin, title);

        cout << "Enter Author Name: ";
        getline(cin, author);

        books.push_back(Book(id, title, author));

        cout << "\nBook Added Successfully!\n";
    }

    void displayBooks()
    {
        if (books.empty())
        {
            cout << "\nNo books available!\n";
            return;
        }

        cout << "\n----- BOOK LIST -----\n";

        for (int i = 0; i < books.size(); i++)
        {
            cout << "\nBook ID: " << books[i].id;
            cout << "\nTitle: " << books[i].title;
            cout << "\nAuthor: " << books[i].author;

            if (books[i].issued)
                cout << "\nStatus: Issued\n";
            else
                cout << "\nStatus: Available\n";
        }
    }

    void issueBook()
    {
        int id;

        cout << "\nEnter Book ID to Issue: ";
        cin >> id;

        for (int i = 0; i < books.size(); i++)
        {
            if (books[i].id == id)
            {
                if (books[i].issued)
                {
                    cout << "\nBook is already issued!\n";
                }
                else
                {
                    books[i].issued = true;
                    cout << "\nBook Issued Successfully!\n";
                }

                return;
            }
        }

        cout << "\nBook not found!\n";
    }

    void returnBook()
    {
        int id;

        cout << "\nEnter Book ID to Return: ";
        cin >> id;

        for (int i = 0; i < books.size(); i++)
        {
            if (books[i].id == id)
            {
                if (!books[i].issued)
                {
                    cout << "\nThis book was not issued!\n";
                }
                else
                {
                    books[i].issued = false;
                    cout << "\nBook Returned Successfully!\n";
                }

                return;
            }
        }

        cout << "\nBook not found!\n";
    }

    void searchByTitle()
    {
        string title;
        cin.ignore();

        cout << "\nEnter Book Title to Search: ";
        getline(cin, title);

        for (int i = 0; i < books.size(); i++)
        {
            if (books[i].title == title)
            {
                cout << "\nBook Found!\n";
                cout << "Book ID: " << books[i].id;
                cout << "\nTitle: " << books[i].title;
                cout << "\nAuthor: " << books[i].author << endl;

                return;
            }
        }

        cout << "\nBook not found!\n";
    }

    void searchByAuthor()
    {
        string author;
        cin.ignore();

        cout << "\nEnter Author Name to Search: ";
        getline(cin, author);

        bool found = false;

        for (int i = 0; i < books.size(); i++)
        {
            if (books[i].author == author)
            {
                cout << "\nBook Found!";
                cout << "\nBook ID: " << books[i].id;
                cout << "\nTitle: " << books[i].title;
                cout << "\nAuthor: " << books[i].author << endl;

                found = true;
            }
        }

        if (!found)
        {
            cout << "\nNo books found by this author!\n";
        }
    }
};


int main()
{
    Library library;

    int choice;

    do
    {
        cout << "\n\n===== LIBRARY MANAGEMENT SYSTEM =====";

        cout << "\n1. Add Book";
        cout << "\n2. Display Books";
        cout << "\n3. Issue Book";
        cout << "\n4. Return Book";
        cout << "\n5. Search by Title";
        cout << "\n6. Search by Author";
        cout << "\n7. Exit";

        cout << "\n\nEnter your choice: ";
        cin >> choice;

        switch (choice)
        {
            case 1:
                library.addBook();
                break;

            case 2:
                library.displayBooks();
                break;

            case 3:
                library.issueBook();
                break;

            case 4:
                library.returnBook();
                break;

            case 5:
                library.searchByTitle();
                break;

            case 6:
                library.searchByAuthor();
                break;

            case 7:
                cout << "\nThank you for using Library Management System!\n";
                break;

            default:
                cout << "\nInvalid Choice! Please try again.\n";
        }

    } while (choice != 7);

    return 0;
}
