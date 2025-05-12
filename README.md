# Projet Docker Zabbix

Belloir Félix - Carre Adrien - Bertrand Tharreau Corentin

## Contenu de l'archive

- `docker-compose.yml` : configuration complète Docker Compose (réseaux internes, healthchecks, Cgroups, agent Zabbix, etc.)
- `.env` : toutes les variables sensibles et paramètres de configuration externes
- `README.md` : ce fichier de documentation

---

## Démarrage rapide

### 1. Lancer tous les conteneurs

```bash
docker compose up -d
```

---

### 2. Accès aux interfaces Web

- Zabbix Web : [http://localhost:8080](http://localhost:8080)
  - **Utilisateur** : `Admin`
  - **Mot de passe** : `zabbix`

- pgAdmin : [http://localhost:5050](http://localhost:5050)
  - **Email** : `admin@epsi.com`
  - **Mot de passe** : `00!vDs5#Li3V`

---

## Vérifications

### PostgreSQL

- ✔️ Service actif avec volume `pgdata`
- ✔️ Pas de port exposé (`ports:` absent)
- ✔️ Réseau `backend` de type `internal`

### Zabbix Web

- ✔️ Accessible en HTTP (port 8080)
- ✔️ Healthcheck actif
- ✔️ Fuseau horaire Europe/Paris configuré

### Zabbix Server

- ✔️ Communique avec la base PostgreSQL
- ✔️ Utilise les variables définies dans `.env`

### Zabbix Agent

- ✔️ Agent actif avec nom déclaré via `ZBX_HOSTNAME=zabbix-server`
- ✔️ Peut être supervisé dans l'interface Zabbix

### pgAdmin

- ✔️ Accessible en HTTP (port 5050)
- ✔️ Volume `pgadmin_data` configuré

### Ressources (Cgroups)

- ✔️ Limites mémoire (`mem_limit`) définies
- ✔️ Pas de swap (`memswap_limit: -1`)
- ✔️ Contrôlables avec `docker stats` ou `docker inspect`

---

## Commandes utiles

- Voir l'état des conteneurs :
```bash
docker ps
```

- Inspecter la RAM utilisée :
```bash
docker stats
```

- Vérifier les limites RAM/swap :
```bash
docker inspect <nom_du_conteneur> | grep -A5 Memory
```

- Relancer un service avec recréation :
```bash
docker compose up -d --force-recreate zabbix-agent
```

---
