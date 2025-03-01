```markdown
# Discord.py Enhanced

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)

高度な機能を備えたDiscord.py拡張フレームワーク

## 🚀 主な機能

- **スマートページネーション**  
  大規模データのインタラクティブなページ管理
- **対話型ダイアログ**  
  確認ダイアログと動的選択メニューの内蔵
- **タスクスケジューラー**  
  柔軟なタイミング設定による定期タスク実行
- **拡張コンテキスト**  
  ユーティリティメソッドを追加した拡張Contextクラス
- **設定管理**  
  ホットリロード可能な.ini形式設定システム
- **拡張機能システム**  
  Jishaku連携による動的なCog読み込み

## ⚙️ インストール

1. リポジトリをクローン
```bash
git clone https://github.com/meowkawaiijp/Discord.py-Enhanced.git
cd Discord.py-Enhanced
```

2. 依存関係をインストール
```bash
pip install -r requirements.txt
```

3. Botを起動
```bash
python bot.py
```

## 💡 基本的な使い方

```python
import discord
from discord.ext import commands
from Dispyplus import EnhancedBot, EnhancedContext, log_execution
config = ConfigManager("config.ini")
intents = discord.Intents.all()
bot = EnhancedBot(
    command_prefix=config.get('Bot', 'prefix', fallback='!'),
    intents=intents,
    config=config
)

@bot.command()
@log_execution()
async def uptime(ctx: EnhancedContext):
    uptime_delta = datetime.datetime.now(datetime.timezone.utc) - ctx.bot.start_time
    hours, remainder = divmod(uptime_delta.total_seconds(), 3600)
    minutes, seconds = divmod(remainder, 60)
    await ctx.success(f"Uptime: {int(hours)}h {int(minutes)}m {int(seconds)}s")

@bot.command()
async def userinfo(ctx: EnhancedContext, member: discord.Member):
    entries = [f"name: {member.name}", f"ID: {member.id}", ...]
    await ctx.paginate(entries, per_page=5)
    
await bot.start(config.get('Bot', 'token'))
```

## 🤝 貢献について

1. リポジトリをフォーク
2. 機能ブランチ作成  
   `git checkout -b feature/新機能`
3. 変更をコミット  
   `git commit -m '新機能を追加'`
4. ブランチにプッシュ  
   `git push origin feature/新機能`
5. プルリクエストを作成

## 📜 ライセンス

MITライセンスで配布されています。詳細は`LICENSE`ファイルを参照してください。
