```
🧠 Telegram bot + userbot combo that indexes channel posts
and provides ultra-fast media searching using MongoDB and Redis.

The bot listens for user queries only in groups and replies
directly with search results (no inline mode).

--------------------------------------------------------------------
🚀 FEATURES
--------------------------------------------------------------------
✅ Fast media search (movies, series, etc.)
✅ MongoDB for indexed message storage
✅ Redis caching for repeated search queries
✅ Pagination for large search results
✅ Replies directly in group (no inline mode)
✅ Admin-only commands for maintenance
✅ Fully async (Pyrogram + Motor)
✅ Ready-to-deploy on Heroku

--------------------------------------------------------------------
⚙️ ENVIRONMENT VARIABLES (from info.py)
--------------------------------------------------------------------
BOT_TOKEN          = Telegram Bot Token
APP_ID             = Telegram API ID
API_HASH           = Telegram API Hash
USER_SESSION       = (optional) Pyrogram user session string
AUTHORIZED_USERS   = Comma-separated admin user IDs
MONGO_URL          = MongoDB connection string
DB_NAME            = Database name (e.g., MediaSearch)
COLLECTION_NAME    = Collection name (e.g., posts)
REDIS_HOST         = Redis host (e.g., localhost)
REDIS_PORT         = Redis port (default 6379)
REDIS_USERNAME     =
REDIS_PASSWORD     =

Example .env file:
----------------------------------------------------
BOT_TOKEN=123456789:ABCDEF-ghijkLMNOPQ
APP_ID=123456
API_HASH=abcd1234efgh5678ijkl9012mnop3456
MONGO_URL=mongodb+srv://user:pass@cluster.mongodb.net/
DB_NAME=MediaSearch
COLLECTION_NAME=posts
REDIS_HOST=127.0.0.1
REDIS_PORT=6379
AUTHORIZED_USERS=123456789,987654321
REDIS_USERNAME     =
REDIS_PASSWORD     =
----------------------------------------------------

--------------------------------------------------------------------
🧠 HOW IT WORKS
--------------------------------------------------------------------
1. The bot listens for new media in linked source channels.
2. Each post is indexed and stored in MongoDB.
3. Users send search queries **in groups only**.
4. The bot checks Redis cache:
     - Cache hit → returns instantly
     - Cache miss → queries MongoDB, then stores result in Redis
5. The bot replies directly in the group (no inline mode).
6. Admins can clear cache, reindex, or reset DB anytime.

⚠️ The bot ignores private messages to prevent spam.

--------------------------------------------------------------------
🧩 COMMANDS
--------------------------------------------------------------------
/start
    → Show help and basic bot info.

/checkbot
    → Display MongoDB & Redis health status.

/search <query>
    → Search for media (group only).

/index <group_id_where_bot_works> <source_chat_id_for_indexing>
    → Link chats for indexing.
      Example:
      /index -1001234567890 -1009876543210
      (Indexes media from the source channel to the specified group.)

/delete <target_group_id> <source_chat_id>
    → Unlink chats and remove indexing link.

/reindex
    → Rebuild index manually from linked channels.

/flushredis
    → Clear Redis cache manually.

/resetdb
    → Drop & rebuild MongoDB database (admin only).

--------------------------------------------------------------------
💾 CACHING & LIMITS
--------------------------------------------------------------------
• Redis TTL auto-expires old search results.  
• Pagination prevents overloading chats.  
• MongoDB queries capped to safe limits.  
• Admins can monitor via /checkbot.

--------------------------------------------------------------------
🧰 INSTALLATION
--------------------------------------------------------------------
# Clone repository
git clone https://github.com/lx-0980/TG-Media-Search.git
cd TG-Media-Search

# Install dependencies
pip install pyrogram tgcrypto motor redis python-dotenv humanize

# Set up environment variables (see .env example)

# Run locally
python3 main.py


--------------------------------------------------------------------
💬 EXAMPLE USAGE
--------------------------------------------------------------------
👥 In a group:
User: /search Avatar  
Bot:  🎬 Found 5 results:  
      1️⃣ result 1 
      2️⃣ result 2 
      [Next ➡️] [⏹ Stop]

💬 In private:
User: /search Avatar  
Bot:  ⚠️ This bot only works in groups. Add it to a group to use search.


TG-Media-Search is a modular Telegram bot that indexes media from
channels and enables fast search through direct group replies.

💬 bot replies directly in the chat with results.

⚙️ Use /index <group_id> <source_chat_id> to link channels for indexing.
    
