import time, json, threading, urllib.request, urllib.parse
from flask import Flask

TOKEN = "8794442629:AAHyo7me-xVpRbXnOr9lD7Mz0nuG3zXVgEw"
URL = f"https://api.telegram.org/bot{TOKEN}/"

app = Flask(__name__)

@app.route('/')
def home():
    return "Mister Bob Elite VIP by @Selymmon en ligne !"

def api(method, data=None):
    if data:
        data = urllib.parse.urlencode(data).encode()
        req = urllib.request.Request(URL + method, data=data)
    else:
        req = urllib.request.Request(URL + method)
    with urllib.request.urlopen(req) as r:
        return json.loads(r.read().decode())

def bot_loop():
    offset = 0
    while True:
        try:
            updates = api(f"getUpdates?offset={offset}&timeout=30")
            for u in updates.get("result", []):
                offset = u["update_id"] + 1
                msg = u.get("message", {})
                text = msg.get("text", "")
                chat_id = msg.get("chat", {}).get("id")
                if not chat_id: continue
                if text.startswith("/start"):
                    api("sendMessage", {"chat_id": chat_id, "text": "🔥 MISTER BOB ELITE VIP by @Selymmon 🔥\n\nEn ligne 24h/24\n/prono - Analyse\n/bankroll - Mise\n/combo - Combo du jour\n/vip - Rejoindre VIP"})
                elif text.startswith("/prono"):
                    try:
                        p=text.split(); e1,e2,c1,cx,c2=p[1],p[2],float(p[3]),float(p[4]),float(p[5]); inv=(1/c1)+(1/cx)+(1/c2); pr1=(1/c1)/inv*100; pr2=(1/c2)/inv*100
                        res=f"✅ GROSSE CONFIANCE {e1}" if pr1>pr2+10 else f"✅ GROSSE CONFIANCE {e2}" if pr2>pr1+10 else "⚠️ MATCH PIÈGE - Double Chance"
                        api("sendMessage", {"chat_id": chat_id, "text": f"⚽ {e1} vs {e2}\n{res}\nProb {pr1:.0f}% vs {pr2:.0f}%"})
                    except:
                        api("sendMessage", {"chat_id": chat_id, "text": "Format: /prono PSG OM 1.9 3.4 4.0"})
                elif text.startswith("/vip"):
                    api("sendMessage", {"chat_id": chat_id, "text": "👑 VIP MISTER BOB - @Selymmon\n5000 FCFA/mois\nContact: @Selymmon"})
                elif text.startswith("/bankroll"):
                    try:
                        b=int(text.split()[1]); api("sendMessage", {"chat_id": chat_id, "text": f"💰 Bank: {b} FCFA\nMise 2%: {b*0.02:.0f}\nMise 5%: {b*0.05:.0f}"})
                    except:
                        api("sendMessage", {"chat_id": chat_id, "text": "Usage: /bankroll 10000"})
                elif text.startswith("/combo"):
                    api("sendMessage", {"chat_id": chat_id, "text": "🔥 COMBO DU JOUR\n1. City WIN 1.65\n2. Barca Over 1.5\nCote 2.45 - @Selymmon"})
            time.sleep(1)
        except: time.sleep(3)

threading.Thread(target=bot_loop, daemon=True).start()
if __name__ == "__main__":
    app.run(host="0.0.0.0", port=10000)
