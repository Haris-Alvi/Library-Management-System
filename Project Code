import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;
import java.util.List;

class Book {
    private String title;
    private String author;
    private String isbn;
    private int availableCopies;

    public Book(String title, String author, String isbn, int availableCopies) {
        this.title = title;
        this.author = author;
        this.isbn = isbn;
        this.availableCopies = availableCopies;
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

    public int getAvailableCopies() {
        return availableCopies;
    }

    public void setAvailableCopies(int availableCopies) {
        this.availableCopies = availableCopies;
    }

    @Override
    public String toString() {
        return title + " by " + author + " (ISBN: " + isbn + ")";
    }
}

class Member {
    private String name;
    private String id;

    public Member(String name, String id) {
        this.name = name;
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public String getId() {
        return id;
    }
}

class Request {
    private Member member;
    private Book book;
    private String status;

    public Request(Member member, Book book) {
        this.member = member;
        this.book = book;
        this.status = "Pending";
    }

    public Member getMember() {
        return member;
    }

    public Book getBook() {
        return book;
    }

    public String getStatus() {
        return status;
    }

    public void setStatus(String status) {
        this.status = status;
    }
}

class Admin {
    private String username;
    private String password;
    private List<Book> books;
    private List<Member> members;
    private List<Request> requests;

    public Admin(String username, String password) {
        this.username = username;
        this.password = password;
        this.books = new ArrayList<>();
        this.members = new ArrayList<>();
        this.requests = new ArrayList<>();
    }

    public boolean login(String username, String password) {
        return this.username.equals(username) && this.password.equals(password);
    }

    public void addBook(Book book) {
        books.add(book);
    }

    public void addMember(Member member) {
        members.add(member);
    }

    public void addRequest(Request request) {
        requests.add(request);
    }

    public List<Book> getBooks() {
        return books;
    }

    public List<Member> getMembers() {
        return members;
    }

    public List<Request> getRequests() {
        return requests;
    }

    public void approveRequest(Request request) {
        if (request.getBook().getAvailableCopies() > 0) {
            request.setStatus("Approved");
            request.getBook().setAvailableCopies(request.getBook().getAvailableCopies() - 1); // Decrease available copies
        } else {
            request.setStatus("Rejected");
        }
    }

    public void returnBook(Request request) {
        request.setStatus("Returned");
        request.getBook().setAvailableCopies(request.getBook().getAvailableCopies() + 1); // Increase available copies
    }
}

public class LibraryManagementSystem {
    private JFrame frame;
    private JPanel panel;
    private JButton adminLoginButton, browseBooksButton, borrowBookButton, returnBookButton, viewStatusButton;
    private Admin admin;

    public LibraryManagementSystem() {
        admin = new Admin("admin", "admin");

        frame = new JFrame("Library Management System");
        panel = new JPanel();
        panel.setLayout(new GridLayout(5, 1));

        adminLoginButton = new JButton("Admin Login");
        browseBooksButton = new JButton("Browse Books");
        borrowBookButton = new JButton("Borrow Book");
        returnBookButton = new JButton("Return Book");
        viewStatusButton = new JButton("View Borrowing Status");

        panel.add(adminLoginButton);
        panel.add(browseBooksButton);
        panel.add(borrowBookButton);
        panel.add(returnBookButton);
        panel.add(viewStatusButton);

        frame.add(panel);
        frame.setSize(400, 400);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);

        adminLoginButton.addActionListener(e -> showAdminLoginDialog());
        browseBooksButton.addActionListener(e -> showBooks());
        borrowBookButton.addActionListener(e -> showBorrowBookDialog());
        returnBookButton.addActionListener(e -> showReturnBookDialog());
        viewStatusButton.addActionListener(e -> showViewStatusDialog());
    }

    private void showAdminLoginDialog() {
        JTextField usernameField = new JTextField();
        JPasswordField passwordField = new JPasswordField();
        Object[] message = {
            "Username:", usernameField,
            "Password:", passwordField
        };

        int option = JOptionPane.showConfirmDialog(frame, message, "Login", JOptionPane.OK_CANCEL_OPTION);
        if (option == JOptionPane.OK_OPTION) {
            String username = usernameField.getText();
            String password = new String(passwordField.getPassword());

            if (admin.login(username, password)) {
                showAdminPanel();
            } else {
                JOptionPane.showMessageDialog(frame, "Invalid login credentials");
            }
        }
    }

    private void showAdminPanel() {
        JFrame adminFrame = new JFrame("Admin Panel");
        JPanel adminPanel = new JPanel();
        adminPanel.setLayout(new GridLayout(3, 1));  // Adjusted to 3 rows after removing the "Change Password" button

        JButton addBookButton = new JButton("Add Book");
        JButton viewRequestsButton = new JButton("View Requests");
        JButton viewMembersButton = new JButton("View Members");

        adminPanel.add(addBookButton);
        adminPanel.add(viewRequestsButton);
        adminPanel.add(viewMembersButton);

        adminFrame.add(adminPanel);
        adminFrame.setSize(400, 400);
        adminFrame.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);
        adminFrame.setVisible(true);

        addBookButton.addActionListener(e -> {
            JTextField titleField = new JTextField();
            JTextField authorField = new JTextField();
            JTextField isbnField = new JTextField();
            JTextField copiesField = new JTextField();

            Object[] message = {
                "Title:", titleField,
                "Author:", authorField,
                "ISBN:", isbnField,
                "Number of Copies:", copiesField
            };

            int option = JOptionPane.showConfirmDialog(adminFrame, message, "Add Book", JOptionPane.OK_CANCEL_OPTION);
            if (option == JOptionPane.OK_OPTION) {
                String title = titleField.getText();
                String author = authorField.getText();
                String isbn = isbnField.getText();
                int copies = Integer.parseInt(copiesField.getText());

                if (!title.isEmpty() && !author.isEmpty() && !isbn.isEmpty() && copies > 0) {
                    admin.addBook(new Book(title, author, isbn, copies));
                    JOptionPane.showMessageDialog(adminFrame, "Book added successfully!");
                } else {
                    JOptionPane.showMessageDialog(adminFrame, "All fields must be filled and copies must be greater than 0!");
                }
            }
        });

        viewRequestsButton.addActionListener(e -> {
            List<Request> requests = admin.getRequests();
            StringBuilder requestList = new StringBuilder("Requests:\n");
            for (Request request : requests) {
                requestList.append(request.getMember().getName())
                           .append(" requested '").append(request.getBook().getTitle())
                           .append("' - Status: ").append(request.getStatus()).append("\n");
            }
            JOptionPane.showMessageDialog(adminFrame, requestList.toString());
        });

        viewMembersButton.addActionListener(e -> {
            List<Member> members = admin.getMembers();
            StringBuilder memberList = new StringBuilder("Members:\n");
            for (Member member : members) {
                memberList.append(member.getName()).append(" (ID: ").append(member.getId()).append(")\n");
            }
            JOptionPane.showMessageDialog(adminFrame, memberList.toString());
        });
    }

    private void showBooks() {
        List<Book> books = admin.getBooks();
        if (books.isEmpty()) {
            JOptionPane.showMessageDialog(frame, "No books available.");
            return;
        }

        StringBuilder bookList = new StringBuilder("Available Books:\n");
        for (Book book : books) {
            if (book.getAvailableCopies() > 0) {
                bookList.append(book.getTitle()).append(" by ").append(book.getAuthor())
                        .append(" (ISBN: ").append(book.getIsbn())
                        .append(") - ").append(book.getAvailableCopies()).append(" copies available\n");
            }
        }
        JOptionPane.showMessageDialog(frame, bookList.toString());
    }

    private void showBorrowBookDialog() {
        List<Book> books = admin.getBooks();
        if (books.isEmpty()) {
            JOptionPane.showMessageDialog(frame, "No books available to borrow.");
            return;
        }

        String[] bookTitles = books.stream()
                                   .filter(book -> book.getAvailableCopies() > 0)
                                   .map(Book::getTitle)
                                   .toArray(String[]::new);

        JComboBox<String> bookComboBox = new JComboBox<>(bookTitles);
        JTextField memberNameField = new JTextField();
        JTextField memberIdField = new JTextField();

        Object[] message = {
            "Select Book:", bookComboBox,
            "Member Name:", memberNameField,
            "Member ID:", memberIdField
        };

        int option = JOptionPane.showConfirmDialog(frame, message, "Borrow Book", JOptionPane.OK_CANCEL_OPTION);
        if (option == JOptionPane.OK_OPTION) {
            String selectedBookTitle = (String) bookComboBox.getSelectedItem();
            String memberName = memberNameField.getText();
            String memberId = memberIdField.getText();

            if (memberName.isEmpty() || memberId.isEmpty()) {
                JOptionPane.showMessageDialog(frame, "Member details cannot be empty.");
                return;
            }

            Book selectedBook = books.stream()
                                     .filter(book -> book.getTitle().equals(selectedBookTitle))
                                     .findFirst()
                                     .orElse(null);

            if (selectedBook != null && selectedBook.getAvailableCopies() > 0) {
                Member member = new Member(memberName, memberId);
                admin.addMember(member);
                Request request = new Request(member, selectedBook);
                admin.addRequest(request);
                admin.approveRequest(request); // Auto-approve for simplicity
                JOptionPane.showMessageDialog(frame, "Book borrowed successfully!");
            } else {
                JOptionPane.showMessageDialog(frame, "Error: Book not available.");
            }
        }
    }

    private void showReturnBookDialog() {
        List<Request> requests = admin.getRequests();
        String[] memberNames = requests.stream()
                                      .map(request -> request.getMember().getName())
                                      .toArray(String[]::new);

        JComboBox<String> memberComboBox = new JComboBox<>(memberNames);

        Object[] message = {
            "Select Member:", memberComboBox
        };

        int option = JOptionPane.showConfirmDialog(frame, message, "Return Book", JOptionPane.OK_CANCEL_OPTION);
        if (option == JOptionPane.OK_OPTION) {
            String selectedMemberName = (String) memberComboBox.getSelectedItem();
            Request request = requests.stream()
                                     .filter(r -> r.getMember().getName().equals(selectedMemberName))
                                     .findFirst()
                                     .orElse(null);

            if (request != null) {
                admin.returnBook(request);
                JOptionPane.showMessageDialog(frame, "Book returned successfully!");
            } else {
                JOptionPane.showMessageDialog(frame, "No borrowing record found.");
            }
        }
    }

    private void showViewStatusDialog() {
        List<Request> requests = admin.getRequests();
        StringBuilder statusList = new StringBuilder("Borrowing Status:\n");
        for (Request request : requests) {
            statusList.append(request.getMember().getName())
                      .append(" requested '").append(request.getBook().getTitle())
                      .append("' - Status: ").append(request.getStatus()).append("\n");
        }
        JOptionPane.showMessageDialog(frame, statusList.toString());
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(LibraryManagementSystem::new);
    }
}

