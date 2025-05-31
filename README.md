# RH_DARK_WEB_BROWSER-V1
RH_TERMUX_DARK_WEB_BROWSER-V1

🙂আসসালামু আলাইকুম🙂
"কেমন আছেন সবাই? আজ আপনাদের জন্য নিয়ে আসলাম RH_DARK_WEB_BROWSER-V1 TERMUX এর ভিতরেই,🌚✔️
---

**📡 Tor + Proxychains + Lynx + Custom Bookmark + History + Onion Search Engine**

---

### 🛠️ STEP 1: আগের মতো প্রয়োজনীয় Tools ইনস্টল করুন

```bash
pkg update && pkg upgrade -y
pkg install tor -y
pkg install proxychains-ng -y
pkg install lynx -y
```

---

### ⚙️ STEP 2: Proxychains কনফিগার করুন

```bash
nano ~/.proxychains/proxychains.conf
```

সেখানে নিচের লাইনটা খুঁজে বের করুন:

```
socks4 127.0.0.1 9050
```

এবং এটিকে পরিবর্তন করুন:

```
socks5 127.0.0.1 9050
```

🔐 Save করুন `Ctrl + X`, তারপর `Y` → `Enter`

---

### 📁 STEP 3: Powerful Browser Script তৈরি করুন

```bash
nano rh-darkweb.sh
```

এবার নিচের সম্পূর্ণ কোডটি লিখুন:

```bash
#!/data/data/com.termux/files/usr/bin/bash

BOOKMARK_FILE="$HOME/.darkweb_bookmarks.txt"
HISTORY_FILE="$HOME/.darkweb_history.txt"

# Function: Show menu
function show_menu() {
  clear
  echo "====================================="
  echo "       🕶️ RH DARK WEB BROWSER V2       "
  echo "====================================="
  echo "1. 🔍 Browse a .onion Site"
  echo "2. ⭐ View Bookmarks"
  echo "3. ➕ Add Bookmark"
  echo "4. 📜 View Browsing History"
  echo "5. 🧠 Search via Dark Web Engine"
  echo "6. ❌ Exit"
  echo "====================================="
}

# Function: Browse Onion URL
function browse_onion() {
  read -p "🔗 Enter .onion URL: " onion_url
  echo "$onion_url" >> "$HISTORY_FILE"
  echo "🔍 Opening $onion_url..."
  sleep 2
  proxychains lynx "$onion_url"
}

# Function: View Bookmarks
function view_bookmarks() {
  echo "📑 Saved Bookmarks:"
  cat "$BOOKMARK_FILE" 2>/dev/null || echo "No bookmarks saved."
  echo ""
  read -p "🔗 Enter URL to browse or press Enter to return: " bm
  if [[ "$bm" != "" ]]; then
    echo "$bm" >> "$HISTORY_FILE"
    proxychains lynx "$bm"
  fi
}

# Function: Add Bookmark
function add_bookmark() {
  read -p "🔗 Enter .onion URL to bookmark: " new_bm
  echo "$new_bm" >> "$BOOKMARK_FILE"
  echo "✅ Bookmark saved!"
  sleep 1
}

# Function: View History
function view_history() {
  echo "🕓 Browsing History:"
  cat "$HISTORY_FILE" 2>/dev/null || echo "No history available."
  echo ""
  read -p "🔗 Enter URL to revisit or press Enter to return: " his
  if [[ "$his" != "" ]]; then
    echo "$his" >> "$HISTORY_FILE"
    proxychains lynx "$his"
  fi
}

# Function: Search Engine
function darkweb_search() {
  echo "📡 Using DuckDuckGo Onion Search..."
  read -p "🔎 Enter search term: " query
  search_url="http://duckduckgogg42xjoc72x3sjasowoarfbgcmvfimaftt6twagswzczad.onion/lite/?q=${query// /+}"
  echo "$search_url" >> "$HISTORY_FILE"
  proxychains lynx "$search_url"
}

# Start Tor
echo "🔄 Starting Tor network..."
tor &> /dev/null &
sleep 15

# Main loop
while true; do
  show_menu
  read -p "📥 Select an option [1-6]: " choice
  case $choice in
    1) browse_onion ;;
    2) view_bookmarks ;;
    3) add_bookmark ;;
    4) view_history ;;
    5) darkweb_search ;;
    6) echo "👋 Exiting..."; pkill tor; exit ;;
    *) echo "❌ Invalid option. Try again." ;;
  esac
  read -p "🔁 Press Enter to return to menu..." dummy
done
```

📁 সেভ করুন: `Ctrl + X` → `Y` → `Enter`

---

### 🔐 STEP 4: স্ক্রিপ্টটি রান করার উপযোগী করুন

```bash
chmod +x rh-darkweb.sh
```

---

## ▶️ STEP 5: ব্রাউজার চালু করুন

```bash
./rh-darkweb.sh
```

---

## ✅ এখন আপনি কী কী করতে পারবেন?

| ফিচার              | বর্ণনা                                            |
| ------------------ | ------------------------------------------------- |
| 🔍 `.onion` ব্রাউজ | যেকোনো .onion লিংক টার্মিনাল থেকেই এক্সেস         |
| ⭐ বুকমার্ক         | আপনার পছন্দের ডার্ক ওয়েব লিংক সংরক্ষণ করুন        |
| 📜 হিস্টোরি        | আগের ব্রাউজ করা সাইটের লিস্ট দেখুন ও revisit করুন |
| 🧠 সার্চ ইঞ্জিন    | DuckDuckGo Onion সার্চ সাপোর্ট                    |

---

## 📡 ডার্ক ওয়েব সার্চ ইঞ্জিন URL

```
http://duckduckgogg42xjoc72x3sjasowoarfbgcmvfimaftt6twagswzczad.onion
```

---

## 🛡️ সতর্কতা

☠️ অবৈধ `.onion` সাইট এড়িয়ে চলুন
☪️ ইসলামবিরোধী ও অপরাধমূলক কার্যক্রম থেকে বিরত থাকুন
🧠 শুধুমাত্র গবেষণা ও নিরাপত্তা বিশ্লেষণের কাজে ব্যবহার করুন

---

## ✊ Created by:

**RH – Cyber Security Master | Muslim Army 🛡️**
**Tools: Tor, Lynx, Proxychains, Termux CLI UI**

---
