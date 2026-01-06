# Express.js To-Do Application

Απαλλακτική εργασία στο μάθημα Υπολογιστικό Λογισμικό

## Περιγραφή

Αυτή είναι μια Express.js εφαρμογή διαχείρισης εργασιών (To-Do) που χρησιμοποιεί SQLite βάση δεδομένων και Sequelize ORM.

## Δομή Project

```
Express/
├── config/
│   └── database.js          # Ρυθμίσεις σύνδεσης SQLite
├── controllers/             # (κενός φάκελος)
├── models/
│   ├── index.js            # Σχέσεις μοντέλων (toDo ↔ toDoItem)
│   ├── toDo.js             # Μοντέλο Todo
│   └── toDoItem.js         # Μοντέλο TodoItem
├── routes/
│   └── postToDo.js         # Routes για todos
├── database.db             # SQLite βάση δεδομένων
├── server.js               # Κεντρικό αρχείο εφαρμογής
├── package.json
└── package-lock.json
```

## Προαπαιτούμενα

- Node.js (v14 ή νεότερη έκδοση)
- npm (Node Package Manager)

## Εγκατάσταση

1. **Κλωνοποίηση του repository**
   ```bash
   git clone <repository-url>
   cd Express
   ```

2. **Εγκατάσταση dependencies**
   ```bash
   npm install
   ```

3. **Εκκίνηση του server**
   ```bash
   npm start
   ```

   Ο server θα τρέξει στο `http://localhost:8000`

## Dependencies

- **express** (^5.2.1) - Web framework
- **sequelize** (^6.37.7) - ORM για βάση δεδομένων
- **sqlite3** (^5.1.7) - SQLite database driver

## API Endpoints

### POST /todos
Δημιουργία νέου todo item

**Request Body:**
```json
{
  "content": "Τίτλος του todo"
}
```

**Response (201):**
```json
{
  "id": 1,
  "title": "Τίτλος του todo",
  "createdAt": "2024-01-05T00:00:00.000Z",
  "updatedAt": "2024-01-05T00:00:00.000Z"
}
```

**Error Response (400):**
```json
{
  "error": "todo with title <τίτλος> already exists"
}
```

## Μοντέλα Δεδομένων

### toDo
- `id` (INTEGER, Primary Key, Auto Increment)
- `title` (STRING, Not Null, Unique)
- `createdAt` (DATE)
- `updatedAt` (DATE)

### toDoItem
- `id` (INTEGER, Primary Key, Auto Increment)
- `content` (STRING, Not Null)
- `completed` (BOOLEAN, Default: false)
- `todoId` (INTEGER, Foreign Key → toDo.id)
- `createdAt` (DATE)
- `updatedAt` (DATE)

**Σχέση:** Ένα `toDo` έχει πολλά `toDoItem` (one-to-many με CASCADE delete)

## Configuration

Η βάση δεδομένων ρυθμίζεται στο `config/database.js`:
- **Dialect:** SQLite
- **Storage:** `./database.db` (στο root του project)
- **Logging:** Disabled

## Scripts

```json
"start": "node server.js"
```

## Συγγραφέας

vaggelis

## License

ISC
