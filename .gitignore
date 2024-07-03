import 'dart:io'; // เพิ่ม import สำหรับใช้งาน stdin

class Book {
  String title;
  String author;
  String isbn;
  int copies;

  Book({required this.title, required this.author, required this.isbn, required this.copies});

  void borrowBook() {
    if (copies > 0) {
      copies--;
      print("ยืมหนังสือ '$title' สำเร็จ");
    } else {
      print("หนังสือ '$title' ไม่มีสำเนาให้ยืม");
    }
  }

  void returnBook() {
    copies++;
    print("คืนหนังสือ '$title' สำเร็จ");
  }
}

class Member {
  String name;
  String memberId;
  List<Book> borrowedBooks = [];

  Member({required this.name, required this.memberId});

  void borrowBook(Book book) {
    if (book.copies > 0) {
      book.copies--;
      borrowedBooks.add(book);
      print("$name ยืมหนังสือ '${book.title}' สำเร็จ");
    } else {
      print("หนังสือ '${book.title}' ไม่มีสำเนาให้ยืม");
    }
  }

  void returnBook(Book book) {
    if (borrowedBooks.contains(book)) {
      borrowedBooks.remove(book);
      book.copies++;
      print("$name คืนหนังสือ '${book.title}' สำเร็จ");
    } else {
      print("$name ไม่ได้ยืมหนังสือ '${book.title}'");
    }
  }
}

class Library {
  List<Book> books = [];
  List<Member> members = [];

  Library() {
    books = [];
    members = [];
  }

  void addBook(Book book) {
    books.add(book);
    print("เพิ่มหนังสือ '${book.title}' สำเร็จ");
  }

  void removeBook(Book book) {
    if (books.contains(book)) {
      books.remove(book);
      print("ลบหนังสือ '${book.title}' สำเร็จ");
    } else {
      print("หนังสือ '${book.title}' ไม่ได้อยู่ในห้องสมุด");
    }
  }

  void registerMember(Member member) {
    members.add(member);
    print("ลงทะเบียนสมาชิก '${member.name}' สำเร็จ");
  }

  Member? getMember(String memberId) {
    try {
      return members.firstWhere((member) => member.memberId == memberId);
    } catch (e) {
      return null; // หรือจัดการข้อผิดพลาดตามที่ต้องการ
    }
  }

  Book? getBook(String isbn) {
    try {
      return books.firstWhere((book) => book.isbn == isbn);
    } catch (e) {
      return null; // หรือจัดการข้อผิดพลาดตามที่ต้องการ
    }
  }

  void borrowBook(String memberId, String isbn) {
    Member? member = getMember(memberId);
    Book? book = getBook(isbn);
    if (member != null && book != null) {
      member.borrowBook(book);
    } else {
      print("ไม่สามารถยืมหนังสือได้ กรุณาตรวจสอบข้อมูล");
    }
  }

  void returnBook(String memberId, String isbn) {
    Member? member = getMember(memberId);
    Book? book = getBook(isbn);
    if (member != null && book != null) {
      member.returnBook(book);
    } else {
      print("ไม่สามารถคืนหนังสือได้ กรุณาตรวจสอบข้อมูล");
    }
  }

  void displayBooks() {
    if (books.isEmpty) {
      print("ยังไม่มีหนังสือในห้องสมุด");
    } else {
      print("รายชื่อหนังสือทั้งหมด:");
      books.forEach((book) {
        print("- ${book.title} (${book.author}), ISBN: ${book.isbn}, จำนวนสำเนา: ${book.copies}");
      });
    }
  }

  void displayMembers() {
    if (members.isEmpty) {
      print("ยังไม่มีสมาชิกที่ลงทะเบียน");
    } else {
      print("รายชื่อสมาชิกทั้งหมด:");
      members.forEach((member) {
        print("- ${member.name} (รหัสสมาชิก: ${member.memberId})");
      });
    }
  }

  void displayMenu() {
    print("เมนู:");
    print("1. เพิ่มหนังสือ");
    print("2. ลบหนังสือ");
    print("3. ลงทะเบียนสมาชิก");
    print("4. ยืมหนังสือ");
    print("5. คืนหนังสือ");
    print("6. แสดงรายชื่อหนังสือทั้งหมด");
    print("7. แสดงรายชื่อสมาชิกทั้งหมด");
    print("8. ออกจากโปรแกรม");
  }

  void runLibrary() {
    while (true) {
      displayMenu();
      stdout.write("กรุณาเลือกทำรายการ (1-8): ");
      String? choice = stdin.readLineSync();

      switch (choice) {
        case '1':
          addBookFromInput();
          break;
        case '2':
          removeBookFromInput();
          break;
        case '3':
          registerMemberFromInput();
          break;
        case '4':
          borrowBookFromInput();
          break;
        case '5':
          returnBookFromInput();
          break;
        case '6':
          displayBooks();
          break;
        case '7':
          displayMembers();
          break;
        case '8':
          print("ออกจากโปรแกรม");
          return;
        default:
          print("โปรดเลือกทำรายการให้ถูกต้อง (1-8)");
      }
    }
  }

  void addBookFromInput() {
    stdout.write("เพิ่มหนังสือ\n");
    stdout.write("ชื่อหนังสือ: ");
    String title = stdin.readLineSync()!;
    stdout.write("ผู้เขียน: ");
    String author = stdin.readLineSync()!;
    stdout.write("ISBN: ");
    String isbn = stdin.readLineSync()!;
    stdout.write("จำนวนสำเนา: ");
    int copies = int.parse(stdin.readLineSync()!);

    Book newBook = Book(title: title, author: author, isbn: isbn, copies: copies);
    addBook(newBook);
  }

  void removeBookFromInput() {
    stdout.write("ลบหนังสือ\n");
    stdout.write("ISBN ของหนังสือที่ต้องการลบ: ");
    String isbn = stdin.readLineSync()!;
    
    Book? bookToRemove = getBook(isbn);
    if (bookToRemove != null) {
      removeBook(bookToRemove);
    } else {
      print("ไม่พบหนังสือที่ต้องการลบ");
    }
  }

  void registerMemberFromInput() {
    stdout.write("ลงทะเบียนสมาชิก\n");
    stdout.write("ชื่อสมาชิก: ");
    String name = stdin.readLineSync()!;
    stdout.write("รหัสสมาชิก: ");
    String memberId = stdin.readLineSync()!;

    Member newMember = Member(name: name, memberId: memberId);
    registerMember(newMember);
  }

  void borrowBookFromInput() {
    stdout.write("ยืมหนังสือ\n");
    stdout.write("รหัสสมาชิก: ");
    String memberId = stdin.readLineSync()!;
    stdout.write("ISBN ของหนังสือที่ต้องการยืม: ");
    String isbn = stdin.readLineSync()!;

    borrowBook(memberId, isbn);
  }

  void returnBookFromInput() {
    stdout.write("คืนหนังสือ\n");
    stdout.write("รหัสสมาชิก: ");
    String memberId = stdin.readLineSync()!;
    stdout.write("ISBN ของหนังสือที่ต้องการคืน: ");
    String isbn = stdin.readLineSync()!;

    returnBook(memberId, isbn);
  }
}

void main() {
  Library library = Library();

  // เพิ่มหนังสือตัวอย่าง
  Book book1 = Book(title: 'พัฒนา IoT บนแพลตฟอร์ม Arduino ด้วย ESP32', author: 'Author 1', isbn: '111', copies: 5);
  Book book2 = Book(title: 'คู่มือ GO Programming Language (GoLang)', author: 'Author 2', isbn: '222', copies: 3);
  library.addBook(book1);
  library.addBook(book2);

  // ลงทะเบียนสมาชิกตัวอย่าง
  Member member1 = Member(name: 'Pannapong Phonprasit', memberId: 'M001');
  library.registerMember(member1);

  // เรียกใช้งานระบบห้องสมุด
  library.runLibrary();

  // แสดงรายชื่อหนังสือทั้งหมด
  library.displayBooks();

  // แสดงรายชื่อสมาชิกทั้งหมด
  library.displayMembers();
}
