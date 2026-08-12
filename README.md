# AI-jarvis-paid-in-progress-
It is in progress 
import os
import sys
import time
import datetime
import webbrowser
import subprocess
import urllib.request
import urllib.parse
import xml.etree.ElementTree as ET
import threading
import re


# ============================================================
#                 VARDAAN AI - JARVIS 3.5
#             NO THIRD-PARTY PYTHON LIBRARIES
# ============================================================


# ----------------------------- COLORS -----------------------------

RESET = "\033[0m"
BOLD = "\033[1m"

RED = "\033[91m"
GREEN = "\033[92m"
YELLOW = "\033[93m"
BLUE = "\033[94m"
MAGENTA = "\033[95m"
CYAN = "\033[96m"
WHITE = "\033[97m"


def enable_colors():
    if os.name == "nt":
        try:
            os.system("")
        except Exception:
            pass


enable_colors()


# ----------------------------- PATHS -----------------------------

HOME = os.path.expanduser("~")

DESKTOP = os.path.join(HOME, "Desktop")
DOWNLOADS = os.path.join(HOME, "Downloads")
DOCUMENTS = os.path.join(HOME, "Documents")
PICTURES = os.path.join(HOME, "Pictures")
VIDEOS = os.path.join(HOME, "Videos")
MUSIC = os.path.join(HOME, "Music")

NOTES_FILE = os.path.join(
    DESKTOP,
    "Vardaan_AI_Notes.txt"
)


# ----------------------------- UI -----------------------------

def clear_screen():
    try:
        os.system("cls" if os.name == "nt" else "clear")
    except Exception:
        pass


def divider(char="=", length=72):
    print(CYAN + char * length + RESET)


def welcome_screen():

    clear_screen()

    print(BOLD + BLUE)

    print("=" * 72)
    print()
    print("                 WELCOME TO VARDAAN AI")
    print()
    print("                      JARVIS 3.5")
    print()
    print("             JUST A RATHER VERY")
    print("             INTELLIGENT SYSTEM")
    print()
    print("=" * 72)

    print(RESET)

    print(
        GREEN +
        "                 ● VARDAAN AI ONLINE"
        +
        RESET
    )

    print()


def show_what_i_can_do():

    print(BOLD + MAGENTA)
    print("-" * 72)
    print("                    WHAT I CAN DO")
    print("-" * 72)
    print(RESET)

    print(
        CYAN +
        "Time | Date | Day | News | Google | YouTube | Canva"
        +
        RESET
    )

    print(
        YELLOW +
        "Gmail | ChatGPT | Search | Notepad | Calculator | Paint"
        +
        RESET
    )

    print(
        GREEN +
        "Downloads | Desktop | Documents | Battery | Wi-Fi"
        +
        RESET
    )

    print(
        BLUE +
        "System Info | Screenshot | Timer | Notes"
        +
        RESET
    )

    print(
        RED +
        "Lock | Sleep | Restart | Recycle Bin | Exit"
        +
        RESET
    )

    print()

    print(
        WHITE +
        "Type HELP for complete commands."
        +
        RESET
    )

    print()


def full_help():

    print()

    divider("=")

    print(
        BOLD +
        YELLOW +
        "                  JARVIS COMMAND CENTER"
        +
        RESET
    )

    divider("-")

    print(CYAN + "TIME / DATE" + RESET)
    print("  time")
    print("  date")
    print("  day")
    print("  date and time")

    print()

    print(CYAN + "NEWS" + RESET)
    print("  news")
    print("  latest news")
    print("  India news")
    print("  world news")

    print()

    print(CYAN + "WEBSITES" + RESET)
    print("  open Google")
    print("  open YouTube")
    print("  open Canva")
    print("  open Gmail")
    print("  open ChatGPT")

    print()

    print(CYAN + "SEARCH" + RESET)
    print("  search Google Python")
    print("  search YouTube Minecraft")

    print()

    print(CYAN + "APPLICATIONS" + RESET)
    print("  open Notepad")
    print("  open Calculator")
    print("  open Paint")
    print("  open CMD")

    print()

    print(CYAN + "FOLDERS" + RESET)
    print("  open Downloads")
    print("  open Desktop")
    print("  open Documents")
    print("  open Pictures")
    print("  open Videos")
    print("  open Music")

    print()

    print(CYAN + "SYSTEM" + RESET)
    print("  battery")
    print("  wifi")
    print("  system info")
    print("  screenshot")

    print()

    print(CYAN + "TOOLS" + RESET)
    print("  timer 10")
    print("  make a note buy a notebook")

    print()

    print(CYAN + "CONTROL" + RESET)
    print("  lock")
    print("  sleep")
    print("  restart")

    print()

    divider("=")


# ============================================================
#                        LANGUAGE
# ============================================================

LANGUAGE = "english"


def select_language():

    global LANGUAGE

    print(BOLD + MAGENTA)
    print("SELECT LANGUAGE")
    print("-" * 40)
    print(RESET)

    print("  [1] 🇮🇳 Hindi")
    print("  [2] 🇬🇧 English")
    print("  [3] 🇮🇳 Hinglish")
    print()

    while True:

        try:
            choice = input(
                BOLD +
                YELLOW +
                "YOUR LANGUAGE : " +
                RESET
            ).strip().lower()

        except (KeyboardInterrupt, EOFError):
            return False

        if choice in ["1", "hindi", "hi"]:

            LANGUAGE = "hindi"
            return True

        if choice in ["2", "english", "en"]:

            LANGUAGE = "english"
            return True

        if choice in ["3", "hinglish"]:

            LANGUAGE = "hinglish"
            return True

        print(
            RED +
            "Please select 1, 2 or 3."
            +
            RESET
        )


# ============================================================
#                       SPEECH OUTPUT
# ============================================================

def speak(text):

    print(
        BOLD +
        GREEN +
        "JARVIS : " +
        RESET +
        str(text)
    )

    if os.name != "nt":
        return

    try:

        safe_text = str(text)

        safe_text = safe_text.replace(
            "'",
            "''"
        )

        ps = (
            "Add-Type -AssemblyName System.Speech; "
            "$v=New-Object System.Speech.Synthesis.SpeechSynthesizer; "
            "$v.Rate=0; "
            "$v.Volume=100; "
            "$v.Speak('" +
            safe_text +
            "')"
        )

        subprocess.run(
            [
                "powershell.exe",
                "-NoProfile",
                "-Command",
                ps
            ],
            stdout=subprocess.DEVNULL,
            stderr=subprocess.DEVNULL,
            timeout=30
        )

    except Exception:
        pass


def reply(english, hindi=None, hinglish=None):

    if LANGUAGE == "hindi" and hindi:
        speak(hindi)

    elif LANGUAGE == "hinglish" and hinglish:
        speak(hinglish)

    else:
        speak(english)


# ============================================================
#                    VOICE RECOGNITION
# ============================================================

def normalize(text):

    text = str(text).strip().lower()

    replacements = {

        "can va": "canva",
        "you tube": "youtube",
        "chat g p t": "chatgpt",
        "wi fi": "wifi",
        "wi-fi": "wifi",

        "गूगल": "google",
        "यूट्यूब": "youtube",
        "कैनवा": "canva",
        "कैलकुलेटर": "calculator",
        "नोटपैड": "notepad",
        "स्क्रीनशॉट": "screenshot",

        "बैटरी": "battery",
        "समय": "time",
        "तारीख": "date",
        "दिन": "day",

        "समाचार": "news",
        "न्यूज़": "news",
        "न्यूज": "news",
        "खबर": "news",
        "खबरें": "news",

        "खोलो": " kholo ",
        "खोलना": " open ",
        "बताओ": " batao ",
        "बताना": " batao ",
    }

    for old, new in replacements.items():
        text = text.replace(old, new)

    return " ".join(text.split())


def listen():

    print()

    print(
        BOLD +
        YELLOW +
        "🎤 LISTENING..."
        +
        RESET
    )

    ps_code = r'''
Add-Type -AssemblyName System.Speech

try {

    $recognizer =
        New-Object System.Speech.Recognition.SpeechRecognitionEngine

    $recognizer.SetInputToDefaultAudioDevice()

    $grammar =
        New-Object System.Speech.Recognition.DictationGrammar

    $recognizer.LoadGrammar($grammar)

    $result =
        $recognizer.Recognize(
            [TimeSpan]::FromSeconds(10)
        )

    if ($result -ne $null) {
        Write-Output $result.Text
    }

    $recognizer.Dispose()

}
catch {
    Write-Output ""
}
'''

    try:

        result = subprocess.run(
            [
                "powershell.exe",
                "-NoProfile",
                "-ExecutionPolicy",
                "Bypass",
                "-Command",
                ps_code
            ],
            capture_output=True,
            text=True,
            encoding="utf-8",
            errors="ignore",
            timeout=15
        )

        text = result.stdout.strip()

        if text:

            print(
                BOLD +
                BLUE +
                "YOU    : " +
                RESET +
                text
            )

            return normalize(text)

        print(
            RED +
            "JARVIS : I could not hear you."
            +
            RESET
        )

        return ""

    except Exception:

        print(
            RED +
            "JARVIS : Microphone could not be accessed."
            +
            RESET
        )

        return ""


# ============================================================
#                         CHROME
# ============================================================

def open_chrome(url=None):

    chrome_paths = [

        os.path.join(
            os.environ.get("PROGRAMFILES", ""),
            "Google",
            "Chrome",
            "Application",
            "chrome.exe"
        ),

        os.path.join(
            os.environ.get("PROGRAMFILES(X86)", ""),
            "Google",
            "Chrome",
            "Application",
            "chrome.exe"
        ),

        os.path.join(
            os.environ.get("LOCALAPPDATA", ""),
            "Google",
            "Chrome",
            "Application",
            "chrome.exe"
        )
    ]

    chrome = None

    for path in chrome_paths:

        if os.path.isfile(path):
            chrome = path
            break

    try:

        if chrome:

            if url:
                subprocess.Popen([chrome, url])
            else:
                subprocess.Popen([chrome])

        else:

            if url:
                webbrowser.open(url)
            else:
                webbrowser.open(
                    "https://www.google.com"
                )

        return True

    except Exception:

        return False


def open_site(name, url):

    if open_chrome(url):

        reply(
            "Opening " + name,
            name + " खोल रहा हूँ।",
            name + " open kar raha hoon."
        )

    else:

        reply(
            "I could not open " + name,
            name + " नहीं खुल पाया।",
            name + " open nahi ho paya."
        )


# ============================================================
#                        WEBSITES
# ============================================================

def open_google():
    open_site(
        "Google",
        "https://www.google.com"
    )


def open_youtube():
    open_site(
        "YouTube",
        "https://www.youtube.com"
    )


def open_canva():
    open_site(
        "Canva",
        "https://www.canva.com"
    )


def open_gmail():
    open_site(
        "Gmail",
        "https://mail.google.com"
    )


def open_chatgpt():
    open_site(
        "ChatGPT",
        "https://chatgpt.com"
    )


# ============================================================
#                           SEARCH
# ============================================================

def google_search(query):

    if not query:

        reply(
            "What should I search?",
            "मैं क्या search करूँ?",
            "Main kya search karun?"
        )

        return

    url = (
        "https://www.google.com/search?q=" +
        urllib.parse.quote_plus(query)
    )

    open_chrome(url)

    reply(
        "Searching Google.",
        "Google पर search कर रहा हूँ।",
        "Google par search kar raha hoon."
    )


def youtube_search(query):

    if not query:

        reply(
            "What should I search on YouTube?",
            "YouTube पर क्या search करूँ?",
            "YouTube par kya search karun?"
        )

        return

    url = (
        "https://www.youtube.com/results?search_query=" +
        urllib.parse.quote_plus(query)
    )

    open_chrome(url)

    reply(
        "Searching YouTube.",
        "YouTube पर search कर रहा हूँ।",
        "YouTube par search kar raha hoon."
    )


# ============================================================
#                       DATE / TIME
# ============================================================

def tell_time():

    now = datetime.datetime.now()

    reply(
        "The time is " +
        now.strftime("%I:%M %p"),

        "अभी समय है " +
        now.strftime("%I:%M %p"),

        "Abhi time hai " +
        now.strftime("%I:%M %p")
    )


def tell_date():

    now = datetime.datetime.now()

    reply(
        "Today's date is " +
        now.strftime("%d %B %Y"),

        "आज की तारीख " +
        now.strftime("%d %B %Y") +
        " है।",

        "Aaj ki date " +
        now.strftime("%d %B %Y") +
        " hai."
    )


def tell_day():

    now = datetime.datetime.now()

    reply(
        "Today is " +
        now.strftime("%A"),

        "आज " +
        now.strftime("%A") +
        " है।",

        "Aaj " +
        now.strftime("%A") +
        " hai."
    )


def tell_datetime():

    now = datetime.datetime.now()

    reply(
        "Today is " +
        now.strftime("%A") +
        ". The date is " +
        now.strftime("%d %B %Y") +
        ". The time is " +
        now.strftime("%I:%M %p"),

        "आज " +
        now.strftime("%A") +
        " है। तारीख " +
        now.strftime("%d %B %Y") +
        " है और समय " +
        now.strftime("%I:%M %p") +
        " है।",

        "Aaj " +
        now.strftime("%A") +
        " hai. Date " +
        now.strftime("%d %B %Y") +
        " hai aur time " +
        now.strftime("%I:%M %p") +
        " hai."
    )


# ============================================================
#                          NEWS
# ============================================================

COUNTRIES = [
    ("India", "India"),
    ("United States", "United States"),
    ("United Kingdom", "United Kingdom"),
    ("China", "China"),
    ("Japan", "Japan"),
    ("Germany", "Germany"),
    ("France", "France"),
    ("Russia", "Russia"),
    ("Australia", "Australia"),
    ("Canada", "Canada")
]


def clean_news_text(text):

    text = re.sub(
        r"<.*?>",
        "",
        str(text)
    )

    text = text.replace("&amp;", "&")
    text = text.replace("&quot;", '"')
    text = text.replace("&#39;", "'")

    return text.strip()


def fetch_country_news(country):

    articles = []

    query = urllib.parse.quote_plus(
        country
    )

    url = (
        "https://news.google.com/rss/search?"
        "q=" +
        query +
        "&hl=en-US&gl=US&ceid=US:en"
    )

    try:

        request = urllib.request.Request(
            url,
            headers={
                "User-Agent":
                "Mozilla/5.0 Vardaan-AI-JARVIS"
            }
        )

        with urllib.request.urlopen(
            request,
            timeout=10
        ) as response:

            data = response.read()

        root = ET.fromstring(data)

        for item in root.findall(
            ".//item"
        ):

            title_element = item.find(
                "title"
            )

            if title_element is None:
                continue

            title = clean_news_text(
                title_element.text or ""
            )

            if title:
                articles.append(title)

            if len(articles) >= 5:
                break

    except Exception:
        pass

    return articles


def show_news():

    clear_screen()

    print(
        BOLD +
        BLUE
    )

    print("=" * 72)
    print("                    📰 VARDAAN NEWS")
    print("=" * 72)

    print(RESET)

    print(
        YELLOW +
        "Fetching latest headlines..."
        +
        RESET
    )

    print()

    total_articles = 0

    for country_name, search_name in COUNTRIES:

        print(
            BOLD +
            GREEN +
            "🌍 " +
            country_name +
            RESET
        )

        print(
            "-" * 60
        )

        articles = fetch_country_news(
            search_name
        )

        if not articles:

            print(
                YELLOW +
                "No headlines available right now."
                +
                RESET
            )

            print()

            continue

        for index, title in enumerate(
            articles,
            start=1
        ):

            print(
                YELLOW +
                str(index) +
                ". " +
                RESET +
                title
            )

        total_articles += len(
            articles
        )

        print()

    print(
        CYAN +
        "Total headlines displayed: " +
        str(total_articles)
        +
        RESET
    )

    print()

    if total_articles:

        reply(
            "I have displayed the latest news.",
            "मैंने latest news दिखा दी है।",
            "Maine latest news dikha di hai."
        )

    else:

        reply(
            "I could not fetch the news right now.",
            "अभी news नहीं मिल पाई।",
            "Abhi news nahi mil payi."
        )

    input(
        BOLD +
        CYAN +
        "\nPress ENTER to return to JARVIS..."
        +
        RESET
    )


# ============================================================
#                         APPLICATIONS
# ============================================================

def open_app(command, name):

    try:

        subprocess.Popen(command)

        reply(
            "Opening " + name,
            name + " खोल रहा हूँ।",
            name + " open kar raha hoon."
        )

    except Exception:

        reply(
            name + " could not be opened.",
            name + " नहीं खुल पाया।",
            name + " open nahi ho paya."
        )


def open_notepad():
    open_app(["notepad.exe"], "Notepad")


def open_calculator():
    open_app(["calc.exe"], "Calculator")


def open_paint():
    open_app(["mspaint.exe"], "Paint")


def open_cmd():
    open_app(["cmd.exe"], "Command Prompt")


def open_explorer():
    open_app(["explorer.exe"], "File Explorer")


# ============================================================
#                         FOLDERS
# ============================================================

def open_folder(path, name):

    try:

        if os.path.exists(path):

            os.startfile(path)

            reply(
                "Opening " + name,
                name + " खोल रहा हूँ।",
                name + " open kar raha hoon."
            )

        else:

            reply(
                name + " folder was not found.",
                name + " folder नहीं मिला।",
                name + " folder nahi mila."
            )

    except Exception:

        reply(
            "I could not open " + name,
            name + " नहीं खुल पाया।",
            name + " open nahi ho paya."
        )


def open_recycle_bin():

    try:

        subprocess.Popen(
            [
                "explorer.exe",
                "shell:RecycleBinFolder"
            ]
        )

        reply(
            "Opening Recycle Bin.",
            "Recycle Bin खोल रहा हूँ।",
            "Recycle Bin open kar raha hoon."
        )

    except Exception:

        reply(
            "I could not open Recycle Bin.",
            "Recycle Bin नहीं खुल पाया।",
            "Recycle Bin open nahi ho paya."
        )


# ============================================================
#                         SYSTEM
# ============================================================

def battery_info():

    try:

        command = (
            "(Get-CimInstance Win32_Battery)"
            ".EstimatedChargeRemaining"
        )

        result = subprocess.run(
            [
                "powershell.exe",
                "-NoProfile",
                "-Command",
                command
            ],
            capture_output=True,
            text=True,
            encoding="utf-8",
            errors="ignore",
            timeout=10
        )

        value = result.stdout.strip()

        if value:

            reply(
                "Your battery is " +
                value +
                " percent.",
                "आपकी battery " +
                value +
                " percent है।",
                "Aapki battery " +
                value +
                " percent hai."
            )

        else:

            reply(
                "Battery information is unavailable.",
                "Battery की जानकारी नहीं मिल पाई।",
                "Battery ki information nahi mil payi."
            )

    except Exception:

        reply(
            "Battery information is unavailable.",
            "Battery की जानकारी नहीं मिल पाई।",
            "Battery ki information nahi mil payi."
        )


def wifi_info():

    try:

        result = subprocess.run(
            [
                "netsh",
                "wlan",
                "show",
                "interfaces"
            ],
            capture_output=True,
            text=True,
            encoding="utf-8",
            errors="ignore",
            timeout=10
        )

        output = result.stdout

        ssid = ""

        for item in output.splitlines():

            item = item.strip()

            if (
                item.lower().startswith("ssid")
                and
                "bssid" not in item.lower()
            ):

                parts = item.split(
                    ":",
                    1
                )

                if len(parts) == 2:

                    ssid = parts[1].strip()

                    break

        if ssid:

            reply(
                "You are connected to " + ssid,
                "आप " + ssid + " Wi-Fi से connected हैं।",
                "Aap " + ssid + " Wi-Fi se connected ho."
            )

        else:

            reply(
                "Wi-Fi information is unavailable.",
                "Wi-Fi की जानकारी नहीं मिल पाई।",
                "Wi-Fi ki information nahi mil payi."
            )

    except Exception:

        reply(
            "Wi-Fi information is unavailable.",
            "Wi-Fi की जानकारी नहीं मिल पाई।",
            "Wi-Fi ki information nahi mil payi."
        )


def system_info():

    try:

        computer = os.environ.get(
            "COMPUTERNAME",
            "Unknown"
        )

        print()

        print(
            CYAN +
            "Computer Name : " +
            RESET +
            computer
        )

        print(
            CYAN +
            "Python        : " +
            RESET +
            sys.version.split()[0]
        )

        print(
            CYAN +
            "Operating Sys : " +
            RESET +
            os.name
        )

        print()

        reply(
            "Your computer name is " + computer,
            "आपके computer का नाम " + computer + " है।",
            "Aapke computer ka naam " + computer + " hai."
        )

    except Exception:

        reply(
            "System information is unavailable.",
            "System की जानकारी नहीं मिल पाई।",
            "System ki information nahi mil payi."
        )


# ============================================================
#                        SCREENSHOT
# ============================================================

def take_screenshot():

    try:

        if not os.path.exists(PICTURES):
            os.makedirs(PICTURES)

        filename = (
            "Vardaan_AI_" +
            datetime.datetime.now().strftime(
                "%Y%m%d_%H%M%S"
            ) +
            ".png"
        )

        path = os.path.join(
            PICTURES,
            filename
        )

        ps = r'''
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$screen =
    [System.Windows.Forms.Screen]::PrimaryScreen

$bitmap =
    New-Object System.Drawing.Bitmap(
        $screen.Bounds.Width,
        $screen.Bounds.Height
    )

$graphics =
    [System.Drawing.Graphics]::FromImage(
        $bitmap
    )

$graphics.CopyFromScreen(
    $screen.Bounds.Location,
    [System.Drawing.Point]::Empty,
    $screen.Bounds.Size
)

$bitmap.Save(
    'PATHHERE',
    [System.Drawing.Imaging.ImageFormat]::Png
)

$graphics.Dispose()
$bitmap.Dispose()
'''

        ps = ps.replace(
            "PATHHERE",
            path.replace("'", "''")
        )

        subprocess.run(
            [
                "powershell.exe",
                "-NoProfile",
                "-Command",
                ps
            ],
            stdout=subprocess.DEVNULL,
            stderr=subprocess.DEVNULL,
            timeout=20
        )

        if os.path.exists(path):

            reply(
                "Screenshot saved successfully.",
                "Screenshot successfully save हो गया।",
                "Screenshot successfully save ho gaya."
            )

            print(
                GREEN +
                "Saved: " +
                path +
                RESET
            )

        else:

            reply(
                "Screenshot could not be saved.",
                "Screenshot save नहीं हो पाया।",
                "Screenshot save nahi ho paya."
            )

    except Exception:

        reply(
            "Screenshot failed.",
            "Screenshot नहीं हो पाया।",
            "Screenshot nahi ho paya."
        )


# ============================================================
#                        POWER CONTROL
# ============================================================

def lock_pc():

    reply(
        "Locking the computer.",
        "Computer lock कर रहा हूँ।",
        "Computer lock kar raha hoon."
    )

    try:

        subprocess.run(
            [
                "rundll32.exe",
                "user32.dll,LockWorkStation"
            ]
        )

    except Exception:
        pass


def sleep_pc():

    reply(
        "Putting the computer to sleep.",
        "Computer को sleep में डाल रहा हूँ।",
        "Computer ko sleep mein daal raha hoon."
    )

    try:

        subprocess.run(
            [
                "rundll32.exe",
                "powrprof.dll,SetSuspendState",
                "0,1,0"
            ]
        )

    except Exception:
        pass


def restart_pc():

    reply(
        "Restarting the computer in ten seconds.",
        "Computer दस सेकंड में restart होगा।",
        "Computer das seconds mein restart hoga."
    )

    try:

        subprocess.Popen(
            [
                "shutdown",
                "/r",
                "/t",
                "10"
            ]
        )

    except Exception:
        pass


# ============================================================
#                           NOTES
# ============================================================

def save_note(text):

    if not text:

        reply(
            "Please tell me what to write.",
            "बताइए क्या लिखना है।",
            "Bataiye kya likhna hai."
        )

        return

    try:

        with open(
            NOTES_FILE,
            "a",
            encoding="utf-8"
        ) as file:

            file.write(
                "[" +
                datetime.datetime.now().strftime(
                    "%d-%m-%Y %I:%M %p"
                ) +
                "] " +
                text +
                "\n"
            )

        reply(
            "Your note has been saved.",
            "आपका note save हो गया।",
            "Aapka note save ho gaya."
        )

    except Exception:

        reply(
            "I could not save the note.",
            "Note save नहीं हो पाया।",
            "Note save nahi ho paya."
        )


# ============================================================
#                           TIMER
# ============================================================

def start_timer(seconds):

    try:
        seconds = int(seconds)

    except Exception:

        reply(
            "Please give a valid number.",
            "कृपया सही number बताइए।",
            "Please sahi number bataiye."
        )

        return

    if seconds <= 0:

        reply(
            "Timer must be greater than zero.",
            "Timer zero से ज्यादा होना चाहिए।",
            "Timer zero se zyada hona chahiye."
        )

        return

    reply(
        "Timer started.",
        "Timer शुरू हो गया।",
        "Timer start ho gaya."
    )

    def worker():

        time.sleep(seconds)

        reply(
            "Sir, your timer is finished.",
            "सर, आपका timer पूरा हो गया।",
            "Sir, aapka timer complete ho gaya."
        )

    threading.Thread(
        target=worker,
        daemon=True
    ).start()


def get_number(text):

    numbers = re.findall(
        r"\d+",
        text
    )

    if numbers:

        try:
            return int(numbers[0])
        except Exception:
            return None

    return None


# ============================================================
#                      COMMAND PROCESSOR
# ============================================================

def process_command(command):

    command = normalize(command)

    if not command:
        return True


    # EXIT

    if command in [
        "exit",
        "quit",
        "close",
        "exit jarvis"
    ]:

        reply(
            "Goodbye sir. Have a great day.",
            "अलविदा सर। आपका दिन शुभ हो।",
            "Goodbye sir. Have a great day."
        )

        return False


    # HELP

    if command in [
        "help",
        "commands",
        "show commands"
    ]:

        full_help()

        return True


    # GREETING

    if command in [
        "hello",
        "hi",
        "hey",
        "namaste"
    ]:

        reply(
            "Hello sir. I am ready.",
            "नमस्ते सर। मैं तैयार हूँ।",
            "Hello sir. Main ready hoon."
        )

        return True


    # NEWS

    if (
        command == "news"
        or
        "latest news" in command
        or
        "news dikhao" in command
        or
        "india news" in command
        or
        "world news" in command
    ):

        show_news()

        return True


    # DATE + TIME

    if (
        "date and time" in command
        or
        "time and date" in command
    ):

        tell_datetime()

        return True


    # TIME

    if (
        command == "time"
        or
        "what is the time" in command
        or
        "current time" in command
        or
        "time batao" in command
    ):

        tell_time()

        return True


    # DATE

    if (
        command == "date"
        or
        "today date" in command
        or
        "today's date" in command
        or
        "todays date" in command
        or
        "date batao" in command
    ):

        tell_date()

        return True


    # DAY

    if (
        command == "day"
        or
        "what day" in command
        or
        "which day" in command
        or
        "day batao" in command
    ):

        tell_day()

        return True


    # WEBSITES

    if "canva" in command:

        open_canva()
        return True


    if (
        "open google" in command
        or
        "google kholo" in command
    ):

        open_google()
        return True


    if (
        "open youtube" in command
        or
        "youtube kholo" in command
    ):

        open_youtube()
        return True


    if "open gmail" in command:

        open_gmail()
        return True


    if (
        "open chatgpt" in command
        or
        "open chat gpt" in command
    ):

        open_chatgpt()
        return True


    # SEARCH

    if command.startswith("search google"):

        query = command[
            len("search google"):
        ].strip()

        google_search(query)

        return True


    if command.startswith("search youtube"):

        query = command[
            len("search youtube"):
        ].strip()

        youtube_search(query)

        return True


    # APPLICATIONS

    if (
        "open notepad" in command
        or
        "notepad kholo" in command
    ):

        open_notepad()
        return True


    if (
        "open calculator" in command
        or
        "calculator kholo" in command
    ):

        open_calculator()
        return True


    if (
        "open paint" in command
        or
        "paint kholo" in command
    ):

        open_paint()
        return True


    if (
        "open cmd" in command
        or
        "cmd kholo" in command
    ):

        open_cmd()
        return True


    if (
        "open explorer" in command
        or
        "file explorer" in command
    ):

        open_explorer()
        return True


    # FOLDERS

    if (
        "downloads" in command
        or
        "download folder" in command
    ):

        open_folder(
            DOWNLOADS,
            "Downloads"
        )

        return True


    if "desktop" in command:

        open_folder(
            DESKTOP,
            "Desktop"
        )

        return True


    if "documents" in command:

        open_folder(
            DOCUMENTS,
            "Documents"
        )

        return True


    if "pictures" in command:

        open_folder(
            PICTURES,
            "Pictures"
        )

        return True


    if "videos" in command:

        open_folder(
            VIDEOS,
            "Videos"
        )

        return True


    if "music" in command:

        open_folder(
            MUSIC,
            "Music"
        )

        return True


    if (
        "recycle bin" in command
        or
        "recyclebin" in command
    ):

        open_recycle_bin()
        return True


    # SYSTEM

    if "battery" in command:

        battery_info()
        return True


    if "wifi" in command:

        wifi_info()
        return True


    if (
        "system info" in command
        or
        "system information" in command
    ):

        system_info()
        return True


    if "screenshot" in command:

        take_screenshot()
        return True


    # POWER

    if (
        command == "lock"
        or
        "lock computer" in command
        or
        "lock pc" in command
    ):

        lock_pc()
        return True


    if (
        command == "sleep"
        or
        "sleep computer" in command
        or
        "sleep pc" in command
    ):

        sleep_pc()
        return True


    if (
        command == "restart"
        or
        "restart computer" in command
        or
        "restart pc" in command
    ):

        restart_pc()
        return True


    # TIMER

    if (
        command.startswith("timer")
        or
        "set timer" in command
        or
        "timer lagao" in command
    ):

        seconds = get_number(command)

        if seconds is not None:
            start_timer(seconds)

        else:

            reply(
                "Please tell me the timer seconds.",
                "Timer के seconds बताइए।",
                "Timer ke seconds bataiye."
            )

        return True


    # NOTES

    if command.startswith("make a note"):

        note = command[
            len("make a note"):
        ].strip()

        save_note(note)

        return True


    if command.startswith("create note"):

        note = command[
            len("create note"):
        ].strip()

        save_note(note)

        return True


    if command.startswith("note "):

        note = command[
            len("note"):
        ].strip()

        save_note(note)

        return True


    # UNKNOWN

    reply(
        "Sorry sir, I did not understand that command.",
        "माफ कीजिए सर, मैं command समझ नहीं पाया।",
        "Sorry sir, main command samajh nahi paya."
    )

    print(
        YELLOW +
        "Type HELP to see available commands."
        +
        RESET
    )

    return True


# ============================================================
#                         VOICE MODE
# ============================================================

def voice_mode():

    welcome_screen()

    print(
        BOLD +
        MAGENTA +
        "MODE : 🎤 VOICE"
        +
        RESET
    )

    print()

    if not select_language():
        return

    print()

    show_what_i_can_do()

    reply(
        "Welcome to Vardaan AI. What can I do for you?",
        "Vardaan AI में आपका स्वागत है। मैं आपके लिए क्या कर सकता हूँ?",
        "Welcome to Vardaan AI. Main aapke liye kya kar sakta hoon?"
    )

    failed = 0

    while True:

        command = listen()

        if not command:

            failed += 1

            if failed >= 2:

                reply(
                    "Please speak clearly.",
                    "कृपया थोड़ा साफ बोलिए।",
                    "Please thoda clearly boliye."
                )

                failed = 0

            continue

        failed = 0

        running = process_command(
            command
        )

        if not running:
            break

        print()
        divider("-")


# ============================================================
#                        TYPING MODE
# ============================================================

def typing_mode():

    welcome_screen()

    print(
        BOLD +
        MAGENTA +
        "MODE : ⌨️ TYPING"
        +
        RESET
    )

    print()

    if not select_language():
        return

    print()

    show_what_i_can_do()

    reply(
        "Welcome to Vardaan AI. What can I do for you?",
        "Vardaan AI में आपका स्वागत है। मैं आपके लिए क्या कर सकता हूँ?",
        "Welcome to Vardaan AI. Main aapke liye kya kar sakta hoon?"
    )

    while True:

        try:

            command = input(
                BOLD +
                BLUE +
                "YOU    : " +
                RESET
            ).strip()

        except (KeyboardInterrupt, EOFError):

            print()

            reply(
                "Goodbye sir.",
                "अलविदा सर।",
                "Goodbye sir."
            )

            break

        if not command:
            continue

        running = process_command(
            command
        )

        if not running:
            break

        print()
        divider("-")


# ============================================================
#                      MODE SELECTION
# ============================================================

def choose_mode():

    welcome_screen()

    print(
        BOLD +
        YELLOW +
        "SELECT HOW YOU WANT TO CONTROL JARVIS"
        +
        RESET
    )

    print()

    print(
        GREEN +
        "  [1] 🎤 VOICE"
        +
        RESET
    )

    print(
        CYAN +
        "  [2] ⌨️ TYPING"
        +
        RESET
    )

    print()

    while True:

        try:

            choice = input(
                BOLD +
                MAGENTA +
                "YOUR CHOICE : " +
                RESET
            ).strip().lower()

        except (KeyboardInterrupt, EOFError):

            return

        if choice in [
            "1",
            "voice",
            "v"
        ]:

            voice_mode()
            break


        if choice in [
            "2",
            "typing",
            "type",
            "t"
        ]:

            typing_mode()
            break


        print(
            RED +
            "Please select 1 for VOICE or 2 for TYPING."
            +
            RESET
        )


# ============================================================
#                           MAIN
# ============================================================

def main():

    choose_mode()


if __name__ == "__main__":

    try:

        main()

    except KeyboardInterrupt:

        print()

        print(
            YELLOW +
            "JARVIS stopped by user."
            +
            RESET
        )

    except Exception as error:

        print()

        divider("=")

        print(
            RED +
            "JARVIS ERROR"
            +
            RESET
        )

        print(
            RED +
            type(error).__name__ +
            ": " +
            str(error)
            +
            RESET
        )

        divider("=")

    finally:

        print()

        try:

            input(
                BOLD +
                CYAN +
                "Press ENTER to close JARVIS..."
                +
                RESET
            )

        except Exception:
            pass
