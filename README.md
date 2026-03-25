# 📚 Book Library Information System - Complete Guide

## Overview
A fully-featured TypeScript-based book library information system that manages books, authors, publishers, genres, and reviews with a clean, service-oriented architecture.

---

## 🎯 System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                   LibraryManager (Main Coordinator)          │
│                  - Central access point                      │
│                  - Delegates to services                     │
└─────────────────┬───────────────────────────────────────────┘
                  │
        ┌─────────┼──────────┬──────────┬──────────┐
        ▼         ▼          ▼          ▼          ▼
    AuthorSvc GenreSvc PublisherSvc BookSvc ReviewSvc
        │         │          │          │          │
        └─────────┼──────────┼──────────┼──────────┘
                  │
        ┌─────────┴────────────────────┐
        ▼                              ▼
    Interfaces/Models          Data (In-Memory/Database)
```

---

## 📋 Implementation Steps

### **Step 1: Define Data Models (Interfaces)**

Create interfaces in `interfaces/` folder to define your data structures:

- **Author Interface** - Represents book authors
  - Properties: id, firstName, lastName, birthYear, nationality, biography, createdAt

- **Genre Interface** - Book categories
  - Properties: id, name, description, createdAt

- **Publisher Interface** - Publishing companies
  - Properties: id, name, country, foundedYear, website, createdAt

- **Book Interface** - Core book entity
  - Properties: id, title, isbn, publishedYear, pageCount, language, authorID, publisherID, genres[], averageRating, totalReviews

- **Review Interface** - User reviews
  - Properties: id, bookID, userName, rating (1-5), comment, createdAt

### **Step 2: Create Service Classes**

Build individual service classes (`services/` folder) for each entity with CRUD operations:

#### **AuthorService**
```typescript
// Methods:
- addAuthor()          // Create new author
- getAuthorById()      // Read author by ID
- getAllAuthors()      // Get all authors
- updateAuthor()       // Update author details
- deleteAuthor()       // Remove author
```

#### **GenreService**
```typescript
// Methods:
- addGenre()           // Add new genre
- getGenreById()       // Get genre
- getGenreByName()     // Search by name
- getAllGenres()       // List all genres
- updateGenre()        // Update genre
- deleteGenre()        // Remove genre
```

#### **PublisherService**
```typescript
// Methods:
- addPublisher()       // Create publisher
- getPublisherById()   // Get publisher
- getAllPublishers()   // List all
- updatePublisher()    // Update details
- deletePublisher()    // Remove publisher
```

#### **BookService**
```typescript
// Methods:
- addBook()            // Create book
- getBookById()        // Get book
- getAllBooks()        // List all books
- searchByTitle()      // Search books
- getBooksByAuthorId() // Filter by author
- getBooksByGenre()    // Filter by genre
- getBooksByPublisherId() // Filter by publisher
- updateBook()         // Update book
- deleteBook()         // Remove book
```

#### **ReviewService**
```typescript
// Methods:
- addReview()               // Add review (validates rating 1-5)
- getReviewById()           // Get review
- getReviewsByBookId()      // Get all reviews for book
- getAverageRating()        // Calculate average rating
- updateReview()            // Update review
- deleteReview()            // Remove review
```

### **Step 3: Create The Main Manager Class**

**LibraryManager** - Central coordinator that delegates to all service classes:

```typescript
class LibraryManager {
  // Contains instances of all services
  // Provides unified interface for all operations
  // Handles complex operations combining multiple services
  // Implements statistics and reporting methods
}
```

**Key Features:**
- Simplified API for library operations
- Automatic rating calculations
- Full-text search capabilities
- Statistics and analytics
- Top-rated and most-reviewed books
- Complete book details with relationships

### **Step 4: Create Usage Example**

Build a comprehensive example (`examples/example.ts`) demonstrating:

1. ✅ Adding authors
2. ✅ Adding genres
3. ✅ Adding publishers
4. ✅ Adding books
5. ✅ Adding reviews
6. ✅ Searching & filtering
7. ✅ Getting ratings
8. ✅ Viewing statistics
9. ✅ Finding top-rated books
10. ✅ Update operations

---

## 🚀 Quick Start Guide

### Installation & Setup

1. **Install TypeScript** (if not already installed):
```bash
npm install -g typescript
```

2. **Compile TypeScript**:
```bash
tsc
```

3. **Run Example**:
```bash
node examples/example.js
```

### Basic Usage Example

```typescript
import { LibraryManager } from './services/LibraryManager';

const library = new LibraryManager();

// Add an author
const author = library.addAuthor({
    firstName: 'Robert',
    lastName: 'Martin',
    birthYear: 1952,
    nationality: 'American',
    biography: 'Renowned software engineer'
});

// Add a genre
const genre = library.addGenre({
    name: 'Programming',
    description: 'Software development'
});

// Add a publisher
const publisher = library.addPublisher({
    name: 'Prentice Hall',
    country: 'USA',
    foundedYear: 1913,
    website: 'https://www.pearson.com'
});

// Add a book
const book = library.addBook({
    title: 'Clean Code',
    isbn: '978-0132350884',
    publishedYear: 2008,
    pageCount: 464,
    language: 'English',
    description: 'Handbook of Agile Software Craftsmanship',
    authorID: author.id,
    publisherID: publisher.id,
    genres: ['Programming']
});

// Add a review
library.addReview({
    bookID: book.id,
    userName: 'John Doe',
    rating: 5,
    comment: 'Excellent book!'
});

// Search for books
const results = library.searchBooksByTitle('Clean');

// Get statistics
const stats = library.getLibraryStatistics();
console.log(stats);
// Output:
// {
//   totalBooks: 1,
//   totalAuthors: 1,
//   totalGenres: 1,
//   totalPublishers: 1,
//   totalReviews: 1,
//   averageBookRating: 5
// }
```

---

## 📁 Project Structure

```
raamatukogu_infosüsteem/
├── interfaces/
│   ├── author.interface.ts
│   ├── genre.interface.ts
│   ├── publisher.interface.ts
│   ├── book.interface.ts
│   └── review.interface.ts
├── services/
│   ├── AuthorService.ts
│   ├── GenreService.ts
│   ├── PublisherService.ts
│   ├── BookService.ts
│   ├── ReviewService.ts
│   └── LibraryManager.ts
├── examples/
│   └── example.ts
├── tsconfig.json
└── README.md
```

---

## 🔑 Key Features

### ✨ Core Features
- **Full CRUD Operations** - Create, Read, Update, Delete for all entities
- **Relationship Management** - Books linked to authors, publishers, genres
- **Review System** - Users can rate and review books (1-5 rating)
- **Search & Filter** - Search by title, author, genre, publisher
- **Rating System** - Automatic calculation of average ratings

### 📊 Analytics Features
- **Library Statistics** - Total books, authors, genres, publishers, reviews
- **Top-Rated Books** - Get most highly-rated books
- **Most-Reviewed Books** - Get books with most reviews
- **Average Ratings** - Per-book and library-wide averages
- **Full Book Details** - Get complete info including related entities

### 🛡️ Data Validation
- **Rating Validation** - Ensures ratings are between 1-5
- **Error Handling** - Proper error messages for invalid operations
- **Type Safety** - Full TypeScript type checking

---

## 🎓 Design Patterns Used

### 1. **Service Layer Pattern**
- Separates business logic from presentation
- Each entity has its own service class
- Easier to maintain and test

### 2. **Facade Pattern**
- `LibraryManager` acts as a facade
- Simplifies complex subsystems
- Single point of access

### 3. **Repository Pattern**
- Each service manages data for its entity
- Abstraction over data storage
- Easy to switch to database later

### 4. **Dependency Injection**
- Services are injected into managers
- Loose coupling between components
- Better testability

---

## 📝 Advanced Usage

### Get Complete Book Details
```typescript
const details = library.getFullBookDetails(bookId);
console.log(details.book.title);
console.log(details.author.firstName);
console.log(details.publisher.name);
console.log(details.reviews);
console.log(details.averageRating);
```

### Search Operations
```typescript
// Search by title
const books = library.searchBooksByTitle('Clean');

// Get books by author
const authorBooks = library.getBooksByAuthor(authorId);

// Get books in genre
const genreBooks = library.getBooksByGenre('Programming');

// Get books by publisher
const pubBooks = library.getBooksByPublisher(publisherId);
```

### Statistics
```typescript
const stats = library.getLibraryStatistics();
const topBooks = library.getTopRatedBooks(5);
const mostReviewed = library.getMostReviewedBooks(5);
const avgRating = library.getBookAverageRating(bookId);
```

---

## 🔄 Data Flow Example

```
User Input
    ↓
LibraryManager (public method)
    ↓
Specific Service (e.g., BookService)
    ↓
Data Storage (in-memory array)
    ↓
Return Result
    ↓
Display to User
```

---

## 🚀 Future Enhancements

1. **Database Integration** - Replace in-memory storage with SQL/NoSQL
2. **User Authentication** - Implement user accounts and authentication
3. **Advanced Search** - Full-text search, filters, sorting
4. **API Server** - REST API using Express.js
5. **GUI Interface** - Web interface using React/Vue
6. **Persistence** - File-based or cloud storage
7. **Recommendations** - Book recommendation engine
8. **Notifications** - Alert system for new releases

---

## 📚 Learning Resources

### TypeScript Concepts Used
- **Interfaces** - Type definitions
- **Classes** - Object-oriented programming
- **Generics** - Flexible type handling
- **Access Modifiers** (private, public) - Encapsulation
- **Arrays & Methods** - Data management
- **Type Safety** - Compile-time error checking

### Design Principles
- **Single Responsibility Principle** - Each class has one job
- **DRY (Don't Repeat Yourself)** - Reusable code
- **SOLID Principles** - Clean architecture

---

## 🎯 Summary

This book library system demonstrates:
- ✅ **Clean Architecture** - Well-organized, maintainable code
- ✅ **Type Safety** - Full TypeScript advantages
- ✅ **CRUD Operations** - Complete data management
- ✅ **Service Layer** - Separation of concerns
- ✅ **Advanced Features** - Search, filters, analytics
- ✅ **Scalability** - Easy to extend with new features
- ✅ **Best Practices** - Industry-standard patterns

---

## 🤝 Contributing

Feel free to extend this system with:
- More features
- Database integration
- API endpoints
- Web interface
- Unit tests

---

**Happy coding! 📚✨**
