# Library Management System Database

This SQL script creates a database and tables for a simple Library Management System. It also includes sample data and stored procedures to query the database.

## Overview

The script performs the following actions:

1.  **Creates a Database:** Creates a new database named `db_LibraryManagement`.
2.  **Creates Tables:** Defines the schema for the following tables:
    *   `tbl_publisher`: Stores publisher information.
    *   `tbl_book`: Stores book information, including a foreign key referencing `tbl_publisher`.
    *   `tbl_library_branch`: Stores library branch information.
    *   `tbl_borrower`: Stores borrower information.
    *   `tbl_book_loans`: Stores information about book loans, including foreign keys referencing `tbl_book`, `tbl_library_branch`, and `tbl_borrower`.
    *   `tbl_book_copies`: Stores information about the number of copies of each book at each branch, including foreign keys referencing `tbl_book` and `tbl_library_branch`.
    *   `tbl_book_authors`: Stores information about book authors, including a foreign key referencing `tbl_book`.
3.  **Populates Tables:** Inserts sample data into each of the tables.
4.  **Creates Stored Procedures:** Defines stored procedures to perform common queries on the database.

## Tables

*   **tbl\_publisher:**
    *   `publisher_PublisherName` (VARCHAR(100), PRIMARY KEY, NOT NULL): Name of the publisher.
    *   `publisher_PublisherAddress` (VARCHAR(200), NOT NULL): Address of the publisher.
    *   `publisher_PublisherPhone` (VARCHAR(50), NOT NULL): Phone number of the publisher.

*   **tbl\_book:**
    *   `book_BookID` (INT, PRIMARY KEY, NOT NULL, IDENTITY(1,1)): Unique ID for the book.
    *   `book_Title` (VARCHAR(100), NOT NULL): Title of the book.
    *   `book_PublisherName` (VARCHAR(100), NOT NULL, FOREIGN KEY referencing `tbl_publisher`): Name of the publisher (foreign key).

*   **tbl\_library\_branch:**
    *   `library_branch_BranchID` (INT, PRIMARY KEY, NOT NULL, IDENTITY(1,1)): Unique ID for the branch.
    *   `library_branch_BranchName` (VARCHAR(100), NOT NULL): Name of the library branch.
    *   `library_branch_BranchAddress` (VARCHAR(200), NOT NULL): Address of the library branch.

*   **tbl\_borrower:**
    *   `borrower_CardNo` (INT, PRIMARY KEY, NOT NULL, IDENTITY(100,1)): Unique card number for the borrower.
    *   `borrower_BorrowerName` (VARCHAR(100), NOT NULL): Name of the borrower.
    *   `borrower_BorrowerAddress` (VARCHAR(200), NOT NULL): Address of the borrower.
    *   `borrower_BorrowerPhone` (VARCHAR(50), NOT NULL): Phone number of the borrower.

*   **tbl\_book\_loans:**
    *   `book_loans_LoansID` (INT, PRIMARY KEY, NOT NULL, IDENTITY(1,1)): Unique ID for the loan.
    *   `book_loans_BookID` (INT, NOT NULL, FOREIGN KEY referencing `tbl_book`): Book ID (foreign key).
    *   `book_loans_BranchID` (INT, NOT NULL, FOREIGN KEY referencing `tbl_library_branch`): Branch ID (foreign key).
    *   `book_loans_CardNo` (INT, NOT NULL, FOREIGN KEY referencing `tbl_borrower`): Borrower card number (foreign key).
    *   `book_loans_DateOut` (VARCHAR(50), NOT NULL): Date the book was loaned out.
    *   `book_loans_DueDate` (VARCHAR(50), NOT NULL): Due date for the book.

*   **tbl\_book\_copies:**
    *   `book_copies_CopiesID` (INT, PRIMARY KEY, NOT NULL, IDENTITY(1,1)): Unique ID for the copy.
    *   `book_copies_BookID` (INT, NOT NULL, FOREIGN KEY referencing `tbl_book`): Book ID (foreign key).
    *   `book_copies_BranchID` (INT, NOT NULL, FOREIGN KEY referencing `tbl_library_branch`): Branch ID (foreign key).
    *   `book_copies_No_Of_Copies` (INT, NOT NULL): Number of copies of the book at the branch.

*   **tbl\_book\_authors:**
    *   `book_authors_AuthorID` (INT, PRIMARY KEY, NOT NULL, IDENTITY(1,1)): Unique ID for the author.
    *   `book_authors_BookID` (INT, NOT NULL, FOREIGN KEY referencing `tbl_book`): Book ID (foreign key).
    *   `book_authors_AuthorName` (VARCHAR(50), NOT NULL): Name of the author.

## Stored Procedures

The script includes several stored procedures to query the database. Here's a brief description of each:

*   `dbo.bookCopiesAtAllSharpstown`:  How many copies of a specified book are owned by the "Sharpstown" branch.
*   `dbo.bookCopiesAtAllBranches`:  How many copies of a specified book are owned by each library branch.
*   `dbo.NoLoans`: Retrieves the names of all borrowers who do not have any books checked out.
*   `dbo.LoanersInfo`: Retrieves book title, borrower's name, and borrower's address for books due today from the "Sharpstown" branch.
*   `dbo.TotalLoansPerBranch`: Retrieves the branch name and the total number of books loaned out from that branch.
*   `dbo.BooksLoanedOut`: Retrieves the names, addresses, and number of books checked out for all borrowers who have more than a specified number of books checked out.
*   `dbo.BookbyAuthorandBranch`: Retrieves the title and number of copies owned by the "Central" branch for books by a specific author.

## How to Use

1.  **Connect to SQL Server:** Connect to your SQL Server instance using a tool like SQL Server Management Studio (SSMS) or Azure Data Studio.
2.  **Create a New Query:** Open a new query window.
3.  **Execute the Script:** Copy and paste the entire contents of the provided SQL script into the query window and execute it.
4.  **Verify Creation:** Verify that the database `db_LibraryManagement` has been created, along with all the tables and stored procedures.
5.  **Run Stored Procedures:** Execute the stored procedures to query the data. For example:

    ```
    EXEC dbo.TotalLoansPerBranch;
    ```
