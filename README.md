import requests
import sys

# Emoji
map_emoji = "🗺️"
ok = "✅"
fail = "❌"

def geoip_lookup(ip):
    print(f"{map_emoji} Geolocalizzazione per IP: {ip}\n")
    try:
        response = requests.get(f"http://ip-api.com/json/{ip}")
        data = response.json()

        if data['status'] == 'success':
            print(f"{ok} IP: {data['query']}")
            print(f"{ok} Paese: {data['country']} ({data['countryCode']})")
            print(f"{ok} Regione: {data['regionName']}")
            print(f"{ok} Città: {data['city']}")
            print(f"{ok} CAP: {data['zip']}")
            print(f"{ok} ISP: {data['isp']}")
            print(f"{ok} Latitudine: {data['lat']}")
            print(f"{ok} Longitudine: {data['lon']}")
            print(f"{ok} Timezone: {data['timezone']}")
        else:
            print(f"{fail} IP non valido o non trovato.")
    except Exception as e:
        print(f"{fail} Errore: {e}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(f"{fail} Uso: python geoip_tracker.py <IP>")
        sys.exit(1)

    geoip_lookup(sys.argv[1])
