# -LibraryManagementSystem
"Library Management System in Java: Streamlining book inventory, user interactions, and transactions for efficient library operations."


import java.util.ArrayList;

import java.util.List;

import java.util.Scanner;

class Book {
    String title;
    String author;
    int publicationYear;
    boolean isCheckedOut;

    public Book(String title, String author, int publicationYear) {
        this.title = title;
        this.author = author;
        this.publicationYear = publicationYear;
        this.isCheckedOut = false;
    }
}

class User {
    String name;
    int userId;
    List<Book> borrowedBooks;

    public User(String name, int userId) {
        this.name = name;
        this.userId = userId;
        this.borrowedBooks = new ArrayList<>();
    }
}

class Library {
    List<Book> books;
    List<User> users;

    public Library() {
        this.books = new ArrayList<>();
        this.users = new ArrayList<>();
    }

    public void addBook(Book book) {
        books.add(book);
    }

    public void addUser(User user) {
        users.add(user);
    }

    public void displayBooks() {
        System.out.println("Available Books:");
        for (int i = 0; i < books.size(); i++) {
            Book book = books.get(i);
            if (!book.isCheckedOut) {
                System.out.println((i + 1) + ". " + book.title + " by " + book.author);
            }
        }
    }

    public void checkOutBook(User user, int bookNumber) {
        if (bookNumber >= 1 && bookNumber <= books.size()) {
            Book book = books.get(bookNumber - 1);
            if (!book.isCheckedOut) {
                book.isCheckedOut = true;
                user.borrowedBooks.add(book);
                System.out.println("Book checked out successfully!");
            } else {
                System.out.println("Book not available for checkout. Current user's information:");
                System.out.println("User ID: " + user.userId);
                System.out.println("User Name: " + user.name);
                System.out.println("Borrowed Books:");
                if (user.borrowedBooks.isEmpty()) {
                    System.out.println("No books borrowed.");
                } else {
                    for (Book borrowedBook : user.borrowedBooks) {
                        System.out.println("- " + borrowedBook.title + " by " + borrowedBook.author);
                    }
                }
            }
        } else {
            System.out.println("Invalid book number.");
        }
    }

    public void returnBook(User user, int bookNumber) {
        if (bookNumber >= 1 && bookNumber <= user.borrowedBooks.size()) {
            Book book = user.borrowedBooks.get(bookNumber - 1);
            book.isCheckedOut = false;
            user.borrowedBooks.remove(book);
            System.out.println("Book returned successfully!");
        } else {
            System.out.println("Invalid book number.");
        }
    }

    public void addNewBook(String title, String author, int publicationYear) {
        Book newBook = new Book(title, author, publicationYear);
        books.add(newBook);
        System.out.println("New book added successfully!");
    }
}

public class LibraryManagementSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Library library = new Library();

        // Sample data with lowercase book titles
        library.addBook(new Book("Java Programming", "John Doe", 2020));
        library.addBook(new Book("Data Structures", "Jane Smith", 2019));
        // ... (previous code)

        library.addBook(new Book("Art of Computer Programming", "Donald Knuth", 1968));
        library.addBook(new Book("Introduction to Algorithms", "Thomas H. Cormen", 2009));
        library.addBook(new Book("Clean Code", "Robert C. Martin", 2008));
        library.addBook(new Book("Code Complete", "Steve McConnell", 1993));
        library.addBook(new Book("Head First Design Patterns", "Eric Freeman", 2004));
        library.addBook(new Book("The Pragmatic Programmer", "Andrew Hunt", 1999));
        library.addBook(new Book("Design Patterns", "Erich Gamma", 1994));
        library.addBook(new Book("Cracking the Coding Interview", "Gayle Laakmann McDowell", 2008));
        library.addBook(new Book("The Mythical Man-Month", "Frederick P. Brooks Jr.", 1975));
        library.addBook(new Book("Structure and Interpretation of Computer Programs", "Harold Abelson", 1984));
        library.addBook(new Book("Database Systems: The Complete Book", "Hector Garcia-Molina", 2001));
        library.addBook(new Book("The C Programming Language", "Brian Kernighan", 1978));
        library.addBook(new Book("Artificial Intelligence: A Modern Approach", "Stuart Russell", 1995));
        library.addBook(new Book("Computer Organization and Design", "David A. Patterson", 2017));
        library.addBook(new Book("Introduction to Machine Learning", "Alpaydin", 2010));
        library.addBook(new Book("Computer Vision: Algorithms and Applications", "Richard Szeliski", 2010));
        library.addBook(new Book("Deep Learning", "Ian Goodfellow", 2016));
        library.addBook(new Book("Natural Language Processing in Action", "Lane, Howard, and Hapke", 2019));
        library.addBook(new Book("Software Engineering: A Practitioner's Approach", "Roger S. Pressman", 1987));
        library.addBook(new Book("Pattern Recognition and Machine Learning", "Christopher M. Bishop", 2006));

        // ... (remaining code)

        library.displayBooks();

        System.out.println("\nEnter user name:");
        String userName = scanner.nextLine();
        User currentUser = new User(userName, library.users.size() + 1);
        library.addUser(currentUser);

        int choice;
        do {
            System.out.println("\nMenu:");
            System.out.println("1. Check out a book");
            System.out.println("2. Return a book");
            System.out.println("3. Display available books");
            System.out.println("4. Add a new book");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    library.displayBooks();
                    System.out.println("\nEnter the number of the book to check out:");
                    int checkoutBookNumber = scanner.nextInt();
                    library.checkOutBook(currentUser, checkoutBookNumber);
                    break;
                case 2:
                    currentUser.borrowedBooks.forEach(book ->
                            System.out.println((currentUser.borrowedBooks.indexOf(book) + 1) + ". " +
                                    book.title + " by " + book.author));
                    System.out.println("\nEnter the number of the book to return:");
                    int returnBookNumber = scanner.nextInt();
                    library.returnBook(currentUser, returnBookNumber);
                    break;
                case 3:
                    library.displayBooks();
                    break;
                case 4:
                    scanner.nextLine(); // Consume the newline character
                    System.out.println("\nEnter new book details:");
                    System.out.print("Title: ");
                    String newBookTitle = scanner.nextLine();
                    System.out.print("Author: ");
                    String newBookAuthor = scanner.nextLine();
                    System.out.print("Publication Year: ");
                    int newPublicationYear = scanner.nextInt();
                    library.addNewBook(newBookTitle, newBookAuthor, newPublicationYear);
                    break;
                case 5:
                    System.out.println("Exiting the Library Management System. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Please enter a valid option.");
            }
        } while (choice != 5);

        scanner.close();
    }
}
