# SAE 4.CYBER.01 — Sécuriser un système d'information
## Filiale : Houston (Texas)

> **SAE encadrée par** : Christophe Borelly & Christophe Quittet  
> **Domaine** : `houston.mswad.us`  
> **Réseau IPv4 interne** : `172.22.0.0/16`  
> **Réseau IPv6 externe** : `FC00:660:6306:2::/64`

---

## Contexte

Ce projet s'inscrit dans le cadre de la SAE 4.CYBER.01 de la formation BUT Réseaux & Télécommunications (parcours Cybersécurité). L'objectif est de **sécuriser l'infrastructure d'une filiale américaine** d'une entreprise multi-sites dont le quartier général est situé à Redmond (Washington), domaine `MSWAD.US`.

Chaque binôme gère une filiale indépendante interconnectée aux autres via un réseau public IPv6.

---

## Architecture réseau

| Élément | Valeur |
|---|---|
| Site | Houston, Texas |
| Domaine AD | `houston.mswad.us` |
| IPv4 interne | `172.22.0.0/16` |
| IPv6 externe | `FC00:660:6306:2::/64` |
| Réseau inter-sites | `FC00:660:6306::/48` (IPv6 only) |

---

## Infrastructure déployée

### Contrôleurs de domaine (Active Directory)
- **DC1** (PDC principal) — Windows Server 2025
- **DC2** (contrôleur de secours) — Windows Server 2025

### Services obligatoires

| Service | Description |
|---|---|
| **Active Directory / LDAPS** | Annuaire centralisé avec LDAP sécurisé (TLS) |
| **DNS** | Résolution de noms interne et intégration AD |
| **PKI** | Autorité de certification interne (certificats X.509) |
| **DHCP** | Attribution automatique des adresses IP |
| **Web HTTPS** | Serveur web avec zone admin authentifiée via LDAPS |
| **Pare-feu** | Stormshield SN210 — filtrage du trafic entrant/sortant |
| **RDP** | Accès distant sécurisé aux serveurs |

### Options implémentées

| Option | Description |
|---|---|
| **Option 1** | Accès Wi-Fi Entreprise (802.1X) |
| **Option 2** | Serveur RADIUS — authentification EAP-PEAP + MSCHAPv2 |
| **Option 3** | VPN IPSec IKEv2 X.509 site-à-site (IPv4 over IPv6) via strongSwan |
| **Option 4** | Accès VPN IPSec EAP « roadwarrior » pour utilisateurs autorisés |

---

## Équipements

- **Hyperviseur** : VirtualBox
- **Switch** : Cisco SG250 (8 ports)
- **Pare-feu** : Stormshield SN210
- **Routeur inter-sites** : Raspberry Pi (Linux, iptables + strongSwan)
- **VMs** : Windows Server 2025, Windows 11 (clients)

---

## Sécurité

L'infrastructure suit les recommandations de l'**ANSSI** (Agence Nationale de la Sécurité des Systèmes d'Information) :

- Chiffrement des flux avec TLS/LDAPS
- Infrastructure à clés publiques (PKI) interne
- Authentification forte (EAP-PEAP, MSCHAPv2, X.509)
- Segmentation réseau et filtrage pare-feu
- Accès distants sécurisés (RDP over VPN, IPSec)
- Réplication des services critiques (DC secondaire, BDD répliquée)

---

## Structure du dépôt

```
SAE-Cyber-Texas/
├── docs/           # Documentation technique et cahier des charges
├── configs/        # Fichiers de configuration (pare-feu, RADIUS, VPN, etc.)
├── scripts/        # Scripts d'automatisation et de déploiement
└── README.md
```

---

## Livrables

- [ ] Cahier des charges infrastructure
- [ ] Document technique (archi, services, tests de sécurité)
- [ ] Preuves de travail (captures, logs)
- [ ] Soutenance technique (13/06/2025 — matin)
- [ ] Soutenance managériale (13/06/2025 — après-midi)
- [ ] Retour d'expérience individuel (portfolio)
