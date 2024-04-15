# library-management
import java.util.ArrayList;
import java.util.List;

class Book {
    private String title;
    private String author;
    private String isbn;
    private boolean available;

    public Book(String title, String author, String isbn) {
        this.title = title;
        this.author = author;
        this.isbn = isbn;
        this.available = true;
    }

    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }

    public String getIsbn() {
        return isbn;
    }

    public boolean isAvailable() {
        return available;
    }

    public void setAvailable(boolean available) {
        this.available = available;
    }

    @Override
    public String toString() {
        return "Title: " + title + ", Author: " + author + ", ISBN: " + isbn + ", Available: " + available;
    }
}

class LibraryUser {
    private int userId;
    private String name;
    private List<Book> checkedOutBooks;

    public LibraryUser(int userId, String name) {
        this.userId = userId;
        this.name = name;
        this.checkedOutBooks = new ArrayList<>();
    }

    public int getUserId() {
        return userId;
    }

    public String getName() {
        return name;
    }

    public List<Book> getCheckedOutBooks() {
        return checkedOutBooks;
    }

    @Override
    public String toString() {
        return "User ID: " + userId + ", Name: " + name;
    }
}

class Library {
    private List<Book> books;
    private List<LibraryUser> users;

    public Library() {
        books = new ArrayList<>();
        users = new ArrayList<>();
    }

    public void addBook(Book book) {
        books.add(book);
    }

    public void addUser(LibraryUser user) {
        users.add(user);
    }

    public boolean checkOutBook(LibraryUser user, Book book) {
        if (books.contains(book) && book.isAvailable()) {
            book.setAvailable(false);
            user.getCheckedOutBooks().add(book);
            return true;
        }
        return false;
    }

    public boolean returnBook(LibraryUser user, Book book) {
        if (user.getCheckedOutBooks().contains(book)) {
            book.setAvailable(true);
            user.getCheckedOutBooks().remove(book);
            return true;
        }
        return false;
    }

    public void listBooks() {
        for (Book book : books) {
            System.out.println(book);
        }
    }

    public void listUsers() {
        for (LibraryUser user : users) {
            System.out.println(user);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Book book1 = new Book("Python Programming", "divya", "123456789");
        Book book2 = new Book("Data Science Fundamentals", "sruthi", "987654321");
        Book book3 = new Book("Data Science ", "pravalika", "8309468903");

        LibraryUser user1 = new LibraryUser(1, "Amar");
        LibraryUser user2 = new LibraryUser(2, "Dhanesh");

        Library library = new Library();
        library.addBook(book1);
        library.addBook(book2);
        library.addBook(book3);


        library.addUser(user1);
        library.addUser(user2);

        library.checkOutBook(user1, book1);
        library.checkOutBook(user2, book3);
        library.checkOutBook(user2, book2);

        library.listBooks();
        library.listUsers();
    }
}
