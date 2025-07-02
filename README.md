#include <iostream>
#include <vector>
#include <string>
#include <cstdlib>  // gia th rand
using namespace std;

// klash vivliou
class Book {
public:
    string title, author;
    int isbn;

    //kataskevasths vivliou
    Book(string t, string a, int i) : title(t), author(a), isbn(i) {}

    // ektypwsh stoixeiwn vivliou
    void print() {
        cout << title << " - " << author << " - ISBN: " << isbn << endl;
    }
};

// klash rafiou
class Shelf {
    vector<Book> books; // dynamikh lista vivliwn
    int capacity;       // megisth xwritikothta

public:
    // kataskevasths me orisma th xwritikothta
    Shelf(int c) : capacity(c) {}

    // topothetish vivliou se rafi
    bool place(Book b) {
        if (books.size() >= capacity) {
            cout << "to rafi einai gemato\n";
            return false;
        }
        books.push_back(b);
        cout << "topothetithike: ";
        b.print();
        return true;
    }

    // afairesh vivliou apo to rafi(tyxaia apo telos)
    bool take() {
        if (books.empty()) {
            cout << "to rafi einai adeio\n";
            return false;
        }
        books.pop_back();
        cout << "afairethike vivlio\n";
        return true;
    }

    // ektypwsh periexomenou toy rafiou
    void print() {
        if (books.empty()) {
            cout << "to rafi einai adeio\n";
        } else {
            for (auto& b : books)
                b.print();
        }
    }
};

// klash vivliothikhs pou exei 5 rafia
class Library {
    Shelf top, middle, bottom;       // ejwterika rafia
    Shelf cab_top, cab_bottom;       // rafia ntoulapiou

public:
    // kataskevasths: dhmiourgei ta rafia me idia xwritikothta
    Library(int cap)
        : top(cap), middle(cap), bottom(cap), cab_top(cap), cab_bottom(cap) {
        cout << "h vivliothikh dhmiourgithike\n";
    }

    // topothetish vivliou se epilegmeno rafi
    bool place_book(int pos, Book b) {
        switch (pos) {
            case 1: cout << "placing book in top shelf\n"; return top.place(b);
            case 2: cout << "placing book in middle shelf\n"; return middle.place(b);
            case 3: cout << "placing book in bottom shelf\n"; return bottom.place(b);
            case 4: cout << "placing book in cabinet top shelf\n"; return cab_top.place(b);
            case 5: cout << "placing book in cabinet bottom shelf\n"; return cab_bottom.place(b);
            default: return false;
        }
    }

    // afairesh vivliou apo epilegmeno rafi
    bool take_book(int pos) {
        switch (pos) {
            case 1: cout << "taking book from top shelf\n"; return top.take();
            case 2: cout << "taking book from middle shelf\n"; return middle.take();
            case 3: cout << "taking book from bottom shelf\n"; return bottom.take();
            case 4: cout << "taking book from cabinet top shelf\n"; return cab_top.take();
            case 5: cout << "taking book from cabinet bottom shelf\n"; return cab_bottom.take();
            default: return false;
        }
    }

    // ektyposh olwn twn rafiwn ths vivliothikhs
    void print() {
        cout << "\n npanw rafi\n"; top.print();
        cout << "\n meseo rafi\n"; middle.print();
        cout << "katw rafi\n"; bottom.print();
        cout << "panw ntoulapi\n"; cab_top.print();
        cout << "katw ntoulapi\n"; cab_bottom.print();
    }
};

int main() {
    int NMax, L, K1, K2;

    // diavasma parametrwn
    cout << "dwse xwritikothta rafiou(NMax): ";
    cin >> NMax;
    cout << "dwse arithmo vivliwn (L): ";
    cin >> L;
    cout << "dwse arithmo topothetisewn (K1): ";
    cin >> K1;
    cout << "dwse arithmo afaireswn (K2): ";
    cin >> K2;

    // dhmiourgia vivliothikhs
    Library lib(NMax);

    // dhmiourgia vivliwn kai apothikeush se vector
    vector<Book> books;
    for (int i = 0; i < L; i++)
        books.push_back(Book("titlos" + to_string(i), "syggrafeas" + to_string(i), 1000 + i));

    // random topothetiseis vivliwn
    for (int i = 0; i < K1 && i < books.size(); i++) {
        int pos = rand() % 5 + 1; //epilogh rafiou apo 1 mexri 5
        lib.place_book(pos, books[i]);
    }

    // tyxaies afaireseis vivliwn
    for (int i = 0; i < K2; i++) {
        int pos = rand() % 5 + 1;
        lib.take_book(pos);
    }

    // emfanish katastashs vivliothikhs
    lib.print();

    return 0;
}
