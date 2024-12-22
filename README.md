# code-Tech-2
class Book:
    def _init_(self, title, author, book_id, is_borrowed=False):
        self.title = title
        self.author = author
        self.book_id = book_id
        self.is_borrowed = is_borrowed

    def _str_(self):
        return f"ID: {self.book_id} | Title: {self.title} | Author: {self.author} | {'Borrowed' if self.is_borrowed else 'Available'}"


class Library:
    def _init_(self):
        self.books = []
    
    def add_book(self, title, author, book_id):
        new_book = Book(title, author, book_id)
        self.books.append(new_book)
        print(f"Book '{title}' by {author} added to the library.")

    def display_books(self):
        if not self.books:
            print("No books available in the library.")
        else:
            print("Books in the library:")
            for book in self.books:
                print(book)

    def borrow_book(self, book_id):
        book = self._find_book(book_id)
        if book:
            if book.is_borrowed:
                print(f"Sorry, the book '{book.title}' is already borrowed.")
            else:
                book.is_borrowed = True
                print(f"You've successfully borrowed the book '{book.title}'.")
        else:
            print(f"Book with ID {book_id} not found.")

    def return_book(self, book_id):
        book = self._find_book(book_id)
        if book:
            if not book.is_borrowed:
                print(f"The book '{book.title}' was not borrowed.")
            else:
                book.is_borrowed = False
                print(f"You've successfully returned the book '{book.title}'.")
        else:
            print(f"Book with ID {book_id} not found.")

    def search_book(self, title=None, author=None):
        found_books = [book for book in self.books if (title.lower() in book.title.lower() if title else True) and 
                       (author.lower() in book.author.lower() if author else True)]
        if found_books:
            for book in found_books:
                print(book)
        else:
            print("No books found with the provided details.")
    
    def _find_book(self, book_id):
        for book in self.books:
            if book.book_id == book_id:
                return book
        return None


def main():
    library = Library()

    while True:
        print("\nWelcome to the Library Management System")
        print("1. Add Book")
        print("2. Display All Books")
        print("3. Borrow Book")
        print("4. Return Book")
        print("5. Search Book")
        print("6. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            title = input("Enter book title: ")
            author = input("Enter book author: ")
            book_id = input("Enter book ID: ")
            library.add_book(title, author, book_id)
        elif choice == "2":
            library.display_books()
        elif choice == "3":
            book_id = input("Enter book ID to borrow: ")
            library.borrow_book(book_id)
        elif choice == "4":
            book_id = input("Enter book ID to return: ")
            library.return_book(book_id)
        elif choice == "5":
            search_choice = input("Search by (1) Title (2) Author: ")
            if search_choice == "1":
                title = input("Enter book title to search: ")
                library.search_book(title=title)
            elif search_choice == "2":
                author = input("Enter book author to search: ")
                library.search_book(author=author)
            else:
                print("Invalid option.")
        elif choice == "6":
            print("Thank you for using the Library Management System!")
            break
        else:
            print("Invalid choice! Please try again.")


if _name_ == "_main_":
    main()
