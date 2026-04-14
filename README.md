# 🎮 DSAQuest

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js](https://img.shields.io/badge/Node.js-18+-green.svg)](https://nodejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue.svg)](https://www.typescriptlang.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15+-blue.svg)](https://www.postgresql.org/)

> A gamified Data Structures & Algorithms learning platform with intelligent challenge mode randomization.

![DSAQuest Banner](docs/images/banner.png)

## ✨ Features

### 🎯 Challenge Mode
- **Intelligent Randomization**: Every challenge generates a fresh, different set of questions
- **Smart Filtering**: Topic-specific, mixed topics, difficulty levels (Easy/Medium/Hard/All)
- **Recency Avoidance**: Prefers questions not seen in the last 7-14 days
- **Difficulty Balance**: Maintains optimal distribution when "All" difficulty is selected
- **Session Persistence**: Same questions remain consistent during an active challenge

### 🏆 Gamification
- **Character System**: Level up your avatar as you learn
- **XP & Levels**: Earn experience points for correct answers
- **Achievements**: Unlock badges for milestones
- **Daily Quests**: Complete daily challenges for bonus rewards
- **Streak System**: Maintain learning streaks

### 📚 Learning Content
- **7 Realms**: Arrays, Linked Lists, Stacks/Queues, Trees/Graphs, Sorting, Searching, Dynamic Programming
- **Multiple Question Types**: Multiple choice, code completion, true/false
- **Detailed Explanations**: Learn from comprehensive answer explanations
- **Hints System**: Get help when you're stuck

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- PostgreSQL 15+
- npm or yarn

### Backend Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/dsaquest.git
cd dsaquest/backend

# Run setup script
chmod +x setup.sh
./setup.sh

# Or manually:
npm install
cp .env.example .env
# Edit .env with your database credentials
npm run db:generate
npm run db:migrate
npm run db:seed
npm run dev
```

The API will be available at `http://localhost:3001`.

### Docker Setup (Alternative)

```bash
cd dsaquest/backend
docker-compose up
```

### Frontend Setup

```bash
cd dsaquest/frontend
npm install
npm run dev
```

The frontend will be available at `http://localhost:5173`.

## 🏗️ Project Structure

```
dsaquest/
├── backend/                 # Node.js + Express API
│   ├── prisma/             # Database schema and migrations
│   ├── src/
│   │   ├── middleware/     # Auth, rate limiting, error handling
│   │   ├── routes/         # API routes
│   │   ├── services/       # Business logic
│   │   ├── app.ts          # Express app configuration
│   │   └── server.ts       # Server entry point
│   ├── Dockerfile
│   ├── docker-compose.yml
│   └── package.json
│
├── frontend/               # React + TypeScript app
│   ├── src/
│   │   ├── components/     # React components
│   │   ├── hooks/          # Custom React hooks
│   │   ├── pages/          # Page components
│   │   ├── store/          # State management
│   │   └── api/            # API client
│   └── package.json
│
└── docs/                   # Documentation
```

## 📡 API Endpoints

### Challenge Mode

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/api/challenges/start` | Start new challenge with randomized questions | ✅ |
| GET | `/api/challenges/:id/question` | Get current question | ✅ |
| POST | `/api/challenges/:id/answer` | Submit answer | ✅ |
| POST | `/api/challenges/:id/abandon` | Abandon challenge | ✅ |
| GET | `/api/challenges/:id/results` | Get challenge results | ✅ |
| GET | `/api/challenges/history` | Get challenge history | ✅ |

### Example: Start a Challenge

```bash
curl -X POST http://localhost:3001/api/challenges/start \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "realmId": "arrays-strings",
    "difficulty": "MEDIUM",
    "questionCount": 10
  }'
```

## 🧠 Challenge Mode Randomization Algorithm

The randomization engine uses a sophisticated scoring system:

### Scoring Factors

| Factor | Impact | Description |
|--------|--------|-------------|
| Base Score | +100 | Starting score for all questions |
| Very Recent (≤7 days) | -60 | Questions seen very recently |
| Recent (≤14 days) | -35 | Questions seen recently |
| Usage Count | -4×usage | Penalty for frequently used questions |
| Fresh Bonus | +25 | Never used before |
| Underused Bonus | +15 | Used less than 3 times |
| Randomness | ±15 | Controlled randomization |

### Difficulty Balance (when "ALL" selected)
- Easy: 35%
- Medium: 45%
- Hard: 20%

## 🛠️ Tech Stack

### Backend
- **Runtime**: Node.js 18+
- **Framework**: Express.js
- **Language**: TypeScript
- **Database**: PostgreSQL
- **ORM**: Prisma
- **Authentication**: JWT
- **Validation**: Zod

### Frontend
- **Framework**: React 18
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **State Management**: Zustand
- **Build Tool**: Vite

## 📝 Environment Variables

### Backend (.env)

```env
NODE_ENV=development
PORT=3001
DATABASE_URL="postgresql://user:pass@localhost:5432/dsaquest"
JWT_SECRET="your-secret-key"
CORS_ORIGINS="http://localhost:5173"
```

### Frontend (.env)

```env
VITE_API_URL=http://localhost:3001
```

## 🧪 Testing

```bash
# Backend tests
cd backend
npm test

# Frontend tests
cd frontend
npm test
```

## 📦 Deployment

### Using Docker

```bash
cd backend
docker-compose up -d
```

### Manual Deployment

1. Set up PostgreSQL database
2. Configure environment variables
3. Run migrations: `npm run db:migrate:prod`
4. Start server: `npm start`

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) for details.

## 🙏 Acknowledgments

- Inspired by LeetCode, HackerRank, and Duolingo
- Built with modern web technologies
- Community-driven question database

## 📞 Support

- 📧 Email: support@dsaquest.com
- 💬 Discord: [Join our community](https://discord.gg/dsaquest)
- 🐛 Issues: [GitHub Issues](https://github.com/yourusername/dsaquest/issues)

---

<p align="center">
  Made with ❤️ by the DSAQuest Team
</p>
"# DSA_academy5" 
