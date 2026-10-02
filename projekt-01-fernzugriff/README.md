## Ziel
  Verschlüsselter Fernzugriff vom MacBook auf den Ubuntu-Heimserver über das
  Internet – ohne Portfreigabe am Router.

## Architektur
  - Client: MacBook Pro (Tailscale + OpenSSH)
  - Server: Ubuntu auf Lenovo-Laptop, Hostname `cdn01`
  - Transport: Tailscale-VPN (WireGuard), Server-Adresse `<TAILSCALE-IP>`
  - Authentifizierung: SSH-Key, kein Passwort-Login

## Umsetzung
  1. Tailscale auf beiden Geräten installiert und im selben Tailnet verbunden 
  2. Bestehendes SSH-Key-Paar wiederverwendet (kein neues nötig)
  3. `~/.ssh/config`: `Host cdn01` mit HostName, User, IdentityFile, IdentitiesOnly
  4. Public Key in `~/.ssh/authorized_keys` eingetragen (Rechte 700/600)

## Prüfung
  - `ssh cdn01` → Login ohne Passwort
  - `hostname` → `cdn01`, `whoami` → `<USER>`

## Gelernte Lektionen
  - Groß-/Kleinschreibung bei Linux-Benutzernamen zählt
  (`sypop` ≠ `syPop` → `Permission denied (publickey)`)
  - `ssh -v` zeigt, welcher Schlüssel angeboten wird (Fehlersuche)
  - Gästelisten-Prinzip: `authorized_keys` ≈ Türsteher-Liste des Servers
