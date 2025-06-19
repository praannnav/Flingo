# Flingo - Modern Java Swing Flashcard App

Flingo is a simple, modern flashcard desktop application built with Java Swing and MySQL. It supports user login/registration, allows you to create, edit, delete, and flip flashcards with a smooth UI.

---

## Features

- **User registration and login** (credentials stored in MySQL)
- **Modern UI** using Java Swing (flat design, modern fonts/colors)
- **Flashcard dashboard** with animated 3D flip effect
- **Add / Edit / Delete flashcards**
- **Language field** for each flashcard

---

## Setup Instructions

### 1. Prerequisites

- Java 8 or higher
- MySQL server (local or remote)
- MySQL JDBC driver (`mysql-connector-java.jar`) on your classpath

### 2. Database Setup

1. Run the following SQL to create the database and tables:

    ```sql
    CREATE DATABASE IF NOT EXISTS flingo;
    USE flingo;

    CREATE TABLE IF NOT EXISTS users (
        id INT AUTO_INCREMENT PRIMARY KEY,
        username VARCHAR(50) UNIQUE NOT NULL,
        password VARCHAR(255) NOT NULL
    );

    CREATE TABLE IF NOT EXISTS flashcards (
        id INT AUTO_INCREMENT PRIMARY KEY,
        user_id INT NOT NULL,
        front_text VARCHAR(255) NOT NULL,
        back_text VARCHAR(255) NOT NULL,
        language VARCHAR(50) NOT NULL,
        FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
    );
    ```

2. Create a MySQL user, or use your existing credentials.

    ```sql
    CREATE USER 'flingo_user'@'localhost' IDENTIFIED BY 'flingo_pass';
    GRANT ALL PRIVILEGES ON flingo.* TO 'flingo_user'@'localhost';
    FLUSH PRIVILEGES;
    ```

### 3. Project Files

Make sure these files are in your project directory:
- `DB.java`
- `User.java`
- `Flashcard.java`
- `ModernLoginFrame.java`
- `ModernDashboardFrame.java`
- `FlashcardPanel.java`
- `Flingo.java`

### 4. Configuration

Edit `DB.java` and set your MySQL username and password:

```java
static final String USER = "flingo_user";      // your MySQL username
static final String PASS = "flingo_pass";      // your MySQL password
```

### 5. Compile and Run

**Compile:**
```sh
javac -cp .;mysql-connector-java.jar *.java
```

**Run:**
```sh
java -cp .;mysql-connector-java.jar Flingo
```

---

## Usage

1. On first launch, register a new account.
2. Log in with your credentials.
3. Add, edit, delete, and flip flashcards on the dashboard.

- **Click** a flashcard to flip it.
- **Edit** or **Delete** using the buttons below each card.
- All your flashcards are stored per user in the database.


## Security Note

Passwords are stored in plain text for demo purposes. For real use, **hash passwords** with a secure algorithm (e.g., bcrypt or SHA-256).

---

## Troubleshooting

- **ClassNotFoundException:** Ensure `mysql-connector-java.jar` is on your classpath.
- **SQL Exception:** Check that MySQL is running and your credentials in `DB.java` are correct.
- **UI issues:** Use Java 8 or higher.

---

