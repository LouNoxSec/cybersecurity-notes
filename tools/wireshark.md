# 🦈 Fiche Outil : Wireshark

## 📌 Présentation & Objectif
* **Qu'est-ce que c'est ?** L'analyseur de paquets (sniffer) open source le plus populaire du marché. Il permet de capturer et d'inspecter en temps réel le trafic circulant sur un réseau informatique à un niveau granulaire.
* **Cas d'usage principal :** Analyse de trafic réseau, diagnostic de pannes, rétro-ingénierie de protocoles et investigation numérique (Network Forensics) lors d'incidents de sécurité.

## ⚙️ Fonctionnement & Caractéristiques Clés
* **Capture en mode promiscuité :** Permet à une interface réseau de capturer l'ensemble des paquets visibles sur le segment réseau, et non seulement ceux qui lui sont destinés.
* **Moteurs de décodage avancés :** Capable d'interpréter des milliers de protocoles (HTTP, DNS, TLS, SMB, TCP/UDP, etc.) du modèle OSI couche 2 à couche 7.
* **Moteur d'export & d'analyse :** Possibilité d'exporter des objets (fichiers, images) directement à partir d'un flux de données capturé.

## ⚡ Commandes & Filtres Essentiels (Cheatsheet)
* **Filtrer par adresse IP source ou destination :**
  `ip.addr == 192.168.1.10`
* **Filtrer un protocole spécifique (ex: HTTP ou DNS) :**
  `http` ou `dns`
* **Isoler une conversation TCP complète (Stream Following) :**
  Clic droit sur un paquet du flux ➡️ *Follow* ➡️ *TCP Stream* (Permet de lire les échanges en clair comme du texte).
* **Filtrer les requêtes contenant un mot-clé (ex: mot de passe) :**
  `http.request.method == "POST"`

## 💡 Astuces & Pièges à Éviter
* **Attention au volume de données :** Sur un réseau actif, les captures grossissent très vite. Utilise des filtres de capture *avant* de lancer l'enregistrement si tu sais exactement quoi cibler.
* **Chiffrement (HTTPS / TLS) :** Wireshark ne pourra pas lire le contenu applicatif d'un trafic chiffré (HTTPS) sans les clés de déchiffrement adéquates (SSL Key Log). Concentre-toi sur les en-têtes non chiffrés, les flux DNS ou les certificats échangés lors de la phase de *handshake*.
