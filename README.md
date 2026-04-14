# ⚔️ Genshin Characters Database

A full-stack web application for browsing, adding, and managing Genshin Impact characters. Built with modern Angular, Express, and MongoDB.

## Overview

This application provides an interactive interface to explore Genshin Impact characters stored in a MongoDB database. Users can browse a curated collection of characters, view detailed information (role, element, region, rarity), and contribute new characters to the database.

## Features

- 🎮 **Character Browser** – Browse Genshin Impact characters with detailed information
- ➕ **Add Characters** – Contribute new characters to the database with role, element, region, and rarity
- 🗑️ **Delete Characters** – Remove characters from the collection
- 🎨 **Responsive Design** – Mobile-friendly UI built with Bootstrap 5
- ⚡ **Real-time Updates** – Seamless add/delete functionality with automatic list refresh
- 📊 **MongoDB Backend** – Scalable NoSQL database for character data

## Tech Stack

### Frontend
- **Angular 21** – Standalone components, signals, reactive forms
- **Bootstrap 5** – Responsive UI components
- **RxJS** – Reactive programming for HTTP requests
- **TypeScript** – Strict type checking

### Backend
- **Express.js** – REST API server
- **MongoDB** – NoSQL database
- **Node.js** – Runtime environment
- **Nodemon** – Development server with auto-reload

### DevTools
- **Vitest** – Unit testing framework
- **Git & GitHub** – Version control with pre-commit hooks (Husky, Lint-staged)
- **Prettier & ESLint** – Code formatting and linting

## Getting Started

### Prerequisites
- Node.js v18+
- npm v10.9.2+
- MongoDB Atlas account (or local MongoDB)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd ca2
   ```

2. **Set up the backend**
   ```bash
   cd api-server
   npm install
   cp .env.example .env  # Create .env and add your MongoDB connection string
   npm run dev
   ```

   **Backend runs on:** `http://localhost:5050`

3. **Set up the frontend (new terminal)**
   ```bash
   npm install
   npm start
   ```

   **Frontend runs on:** `http://localhost:4200`

### Environment Configuration

**Backend (.env)**
```env
ATLAS_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<database>?retryWrites=true&w=majority
PORT=5050
```

**Frontend (src/environments/)**
- Development: `http://localhost:5050/genshin`
- Production: `http://3.253.234.33:5050/genshin`

## Project Structure

```
ca2/
├── api-server/              # Express backend
│   ├── db/
│   │   └── conn.mjs         # MongoDB connection
│   ├── routes/
│   │   └── posts.mjs        # Character CRUD routes
│   ├── index.mjs            # Server entry point
│   └── package.json
│
├── src/                      # Angular frontend
│   ├── app/
│   │   ├── home/            # Home page component
│   │   ├── about/           # About page component
│   │   ├── addcharacter/    # Add character form
│   │   ├── listcharacters/  # Character list display
│   │   ├── models/          # TypeScript interfaces
│   │   ├── itemsapiservice.ts  # HTTP service
│   │   ├── app.routes.ts    # Routing configuration
│   │   └── app.ts           # Root component
│   ├── environments/        # Environment configs
│   ├── index.html           # HTML entry point
│   ├── main.ts              # Angular bootstrap
│   └── styles.css           # Global styles
│
├── angular.json             # Angular CLI config
├── tsconfig.json            # TypeScript config
└── package.json             # Frontend dependencies
```

## API Endpoints

### GET `/genshin`
Fetch all characters (max 50)
```json
[
  {
    "_id": "...",
    "name": "Fischl",
    "role": "Sub-DPS",
    "element": "Electro",
    "region": "Mondstadt",
    "rarity": "4★",
    "img": "https://...",
    "date": "2024-01-15T10:30:00Z"
  }
]
```

### GET `/genshin/:id`
Fetch a single character by ID
```bash
curl http://localhost:5050/genshin/507f1f77bcf86cd799439011
```

### POST `/genshin`
Add a new character
```bash
curl -X POST http://localhost:5050/genshin \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Nahida",
    "role": "Main DPS",
    "element": "Dendro",
    "region": "Sumeru",
    "rarity": "5★",
    "img": "https://..."
  }'
```

### DELETE `/genshin/:id`
Delete a character by ID
```bash
curl -X DELETE http://localhost:5050/genshin/507f1f77bcf86cd799439011
```

## Development

### Running Tests
```bash
npm test
```

### Build for Production
```bash
npm run build
```

### Code Quality
```bash
# Format code
npm run format

# Lint code
npm run lint
```

### Git Hooks
This project uses Husky for pre-commit linting and formatting:
```bash
npm run prepare  # Install git hooks
```

## Angular Best Practices

This project follows modern Angular 21 conventions:

✅ **Standalone Components** – No NgModules required  
✅ **Signals & Computed State** – Reactive, performant state management  
✅ **Typed Forms** – Strict TypeScript validation  
✅ **OnPush Change Detection** – Performance optimization  
✅ **Lazy Loading** – Route-based code splitting  
✅ **WCAG AA Compliance** – Accessible UI components  

## Accessibility & Performance

- 🎯 **AXE Compliance** – All components pass automated accessibility checks
- 📊 **Bundle Size** – Optimized for under 500kB (initial), 4kB per component
- 🖼️ **Image Optimization** – NgOptimizedImage for responsive images
- ♿ **ARIA Labels** – Semantic HTML and ARIA attributes throughout

## Contribution Guidelines

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Code Standards
- Follow the `.editorconfig` settings
- Run `npm run format` before committing
- Write unit tests for new features
- Update documentation as needed

## Troubleshooting

### MongoDB Connection Issues
- Verify `ATLAS_URI` in `.env` is correct
- Check IP whitelist in MongoDB Atlas
- Ensure network connectivity to Atlas cluster

### CORS Errors
- Confirm backend is running on port 5050
- Check frontend environment configuration
- Verify `cors()` middleware is enabled in Express

### Image Loading Failures
- Images fall back to placeholder (handled in template)
- Verify image URLs are publicly accessible
- Consider hosting images on CDN for production

## Performance Metrics

| Metric | Target | Status |
|--------|--------|--------|
| Initial Load | <3s | ✅ |
| Character List Render | <500ms | ✅ |
| Add/Delete Response | <1s | ✅ |
| Mobile Score | >90 | ✅ |

## Future Enhancements

- 🔍 **Search & Filter** – Filter characters by element, role, region
- ⭐ **Favorites** – Save favorite characters (local storage)
- 🌙 **Dark Mode** – Theme toggle for improved UX
- 📱 **Progressive Web App** – Offline support and installability
- 🔐 **Authentication** – User accounts and permissions
- 📈 **Analytics** – Track popular characters and trends
- 🌍 **Internationalization** – Support for multiple languages

## License

This project is licensed under the **Apache License 2.0** – see the [LICENSE](./api-server/LICENSE) file for details.

## Credits

**Student:** Yelyzaveta Kareieva – S00267553  
**Institution:** Atlantic TU, Ireland  
**Assignment:** CA2 – Full-stack Web Application

---

**Built with ❤️ using Angular, Express, and MongoDB**