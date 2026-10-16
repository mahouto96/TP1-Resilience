# TP1 - Resilience avec HAProxy

Ce projet met en place deux serveurs web Nginx derriere un proxy HAProxy. HAProxy distribue les requetes entre les serveurs et retire temporairement un serveur du pool si son controle de sante echoue.

## Prerequis

- Docker avec Docker Compose

## Demarrer

Depuis le dossier du projet :

```powershell
docker compose up -d
```

Compose attend que les controles de sante des deux serveurs web reussissent avant de demarrer le proxy.

## Tester

- Site web : <http://localhost:8088>
- Statistiques HAProxy : <http://localhost:8404/stats>

Les statistiques sont sans authentification. Le port est publie uniquement sur `127.0.0.1` ; elles restent donc accessibles depuis la machine locale.

Pour verifier la repartition, actualisez plusieurs fois le site et comparez les pages servies par `web1` et `web2`.

Pour verifier la resilience, arretez un serveur puis rechargez le site :

```powershell
docker compose stop web1
```

Le proxy doit continuer a repondre avec `web2`. Pour retablir les deux serveurs :

```powershell
docker compose start web1
```

Afficher l'etat des services et les journaux :

```powershell
docker compose ps
docker compose logs -f
```

## Arreter

```powershell
docker compose down
```
