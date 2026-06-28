# Oldschool Runescape "World" Style Task Generator
An external game I made for my community of 400+ members.

<div align="center">

[![Discord](https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/your-server)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com)
[![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://mongodb.com)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://docker.com)

[🎮 Features](#features) • [🏗️ Architecture](#architecture) • [🚀 Quick Start](#quick-start) • [📚 Documentation](#documentation)

</div>

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/dc12903e-8a69-4cc5-8222-e6110b09734d" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3dc0b163-e053-4527-a49e-6f5aa9fc8532" />
<img width="646" height="753" alt="image" src="https://github.com/user-attachments/assets/d32d42ab-50ef-47e4-9930-0f1db14e486f" />

---

## Features

### Core Gaming Mechanics
- **Progressive World System**: 4 unique worlds with escalating difficulty and specialized mechanics
- **Dynamic Tile Generation**: Procedurally shuffled tile layouts for unknown, non-leakable fair competition
- **Complex, Fun Trial Systems**: Multi-stage key trials with branching paths and strategic decision-making
- **Boss Encounters**: High-stakes finale challenges requiring team coordination
- **Smart Cooldown Management**: Ranking-based skip timers to maintain competitive balance

### Discord Integration
- **Slash Commands**: Modern Discord.py implementation with autocomplete and validation
- **Media Submission System**: Seamless image upload and approval workflows
- **Real-Time Notifications**: Contextual embeds with rich formatting and visual feedback
- **Persistent View Components**: Stateful UI elements that survive bot restarts

### Technical Infrastructure
- **Containerized Deployment**: Full Docker Compose stack for easy scaling and maintenance
- ** MongoDB Integration**: Optimized data models for complex team state management
- **Dynamic Image Processing**: On-demand board generation with custom fonts and overlays
- **RESTful API Design**: Clean separation between Discord bot and game logic
- **Comprehensive Error Handling**: Graceful degradation and user-friendly error messages

## Documentation

### Command Reference

#### Player Commands
| Command | Description | Usage |
|---------|-------------|-------|
| `/board` | View current team board | Available in team channels only |
| `/submit` | Submit tile completion | `/submit option:[1-5] image:[attachment]` |
| `/skip` | Skip current tile | Cooldown varies by ranking |

#### Admin Commands
| Command | Description | Usage |
|---------|-------------|-------|
| `/admin_register` | Register new team | `/admin_register team_name user1 user2 ...` |
| `/admin_view_board` | View any team's board | `/admin_view_board @user` |
| `/admin_force_complete` | Force complete tile | Emergency admin tool |
| `/admin_create_leaderboard` | Initialize leaderboard | Creates auto-updating message |

### Game Mechanics Deep Dive

#### World Progression System
```
World 1: Mystic Cove → 18 tiles + 5 key trials + boss
World 2: Scarab's Labyrinth → 20 tiles + branching path trials + boss  
World 3: Icy Path → 16 tiles + brazier lighting system + boss
World 4: Drakan's Shade → 20 tiles + void trials + final boss
```

#### Submission Workflow
1. **Player Submission**: Image upload with option selection
2. **Admin Review**: Reaction-based approval in dedicated channel
3. **State Update**: Automatic progression and embed updates
4. **Notification**: Team and leaderboard updates

#### Ranking & Cooldowns
- **1st Place**: No skipping allowed (maintains competitive integrity)
- **2nd-5th Place**: 16-hour skip cooldown
- **6th+ Place**: 12-hour skip cooldown

---

## 🛠️ Development

### Project Structure
```
SummerBingo/
├── discord_bot/                 # Discord.py bot implementation
│   ├── cogs/                   # Modular command handlers
│   ├── views/                  # Persistent UI components  
│   ├── utils/                  # Helper functions
│   └── enums/                  # Type definitions
├── game_service_api/           # Flask REST API
│   ├── controllers/            # API endpoints
│   ├── models/                 # Data models
│   ├── services/               # Business logic
│   └── constants/              # Game configuration
├── planning/                   # Game design documents
└── sample_api_requests/        # API testing suite
```

### Key Design Patterns

#### Command Pattern Implementation
```python
# Clean separation of concerns in cog architecture
class PlayerCog(commands.Cog):
    @app_commands.command(name="submit")
    async def submit(self, interaction, option: int, image: discord.Attachment):
        # Handles complex submission logic with state validation
```

#### Observer Pattern for Real-Time Updates
```python
# Auto-updating leaderboard with 3-minute refresh cycle
@tasks.loop(minutes=3)
async def update_leaderboard(self):
    # Fetches latest team data and updates Discord embed
```

#### Factory Pattern for Dynamic Content
```python
# Dynamic embed generation based on game state
def get_embed_for_board(self, team_data: Dict, board_info: Dict):
    # Returns appropriate embed type based on world and game state
```

### Database Schema
```javascript
// Team Document Structure
{
  _id: ObjectId,
  team_name: String,
  discord_channel_id: String,
  players: [Player],
  current_world: Number,
  current_tile: Number,
  game_state: Number, // 0=overworld, 1=key, 2=boss
  completion_counter: Number,
  last_rolled_at: Date,
  // World-specific progression data
  w1_shuffled_tiles: [Number],
  w2_path_chosen: Number,
  w3_braziers_lit: Number,
  // ... extensive state tracking
}
```

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built with ❤️ for the Discord community**

*Showcasing modern Discord bot development practices and enterprise-grade architecture*

</div>
