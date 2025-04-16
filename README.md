# grpc-ws-reverse-proxy
Reverse Proxy WebSocket avec microservice gRPC

##  Objectifs
L'objectif de ce projet est de mettre en place une infrastructure permettant d'échanger des messages en temps réel via un service gRPC et un proxy WebSocket. Cela permet de :
-  Définir un service gRPC via un fichier .proto
-  Développer un serveur gRPC en Node.js pour gérer les communications
-  Mettre en place un reverse proxy WebSocket pour relayer les messages entre clients et serveur gRPC

## Outils utilisés
- **Node.js**
- **Protocol Buffers (Protobuf)**
- **@grpc/grpc-js**
- **@grpc/proto-loader**
- **ws (WebSocket)**

---

## Etape 1: Installation

### 1. Cloner le projet
```bash
git clone https://github.com/amalbenalii/grpc-ws-reverse-proxy.git
cd grpc-ws-reverse-proxy
```

###  2. Initialiser le projet Node.js
```bash
npm init -y

```

###  3. Installer les dépendances
```bash
npm install @grpc/grpc-js @grpc/proto-loader ws

```
---
##  Structure du projet
```
grpc-ws-reverse-proxy/
├── client.html               # Client Web simple pour tester la connexion WebSocket
├── chat.proto                # Définition du service gRPC (Protobuf)
├── server.js                 # Serveur gRPC qui implémente le service Chat
├── proxy.js                  # Reverse Proxy WebSocket qui relaie les messages vers gRPC
├── package.json              # Dépendances et configuration du projet Node.js
└── README.md                 # Documentation du projet

```
---
##  Etape 2: Lancement

1. Démarrer le serveur gRPC :
```bash
node server.js
```
Le serveur démarre sur 0.0.0.0:50051 et mplémente 2 méthodes principales :

- **GetUser**: Récupère les informations d'un utilisateur

- **Chat**: Gère le streaming bidirectionnel des messages


2. Démarrer le reverse proxy WebSocket :
```bash
node proxy.js
```
Le proxy est accessible via ws://localhost:8080 qui fait le lien entre WebSocket et gRPC pour échanger les messages

---

##  Etape 3: Test avec Postman

1. Ouvrir Postman et créer une requête WebSocket sur ws://localhost:8080
2. Envoyer un message JSON :
```json
{
  "chat_message": {
    "id": "msg1",
    "room_id": "room1",
    "sender_id": "client1",
    "content": "Hello World !"
  }
}
```

---

## Fonctionnalités supplémentaires

### 1. Historique des messages
- Ajout de la méthode `GetChatHistory` dans `chat.proto`
- Mémorisation des messages côté serveur
- Mise à jour du proxy pour supporter cette fonctionnalité

### 2. Client Web 
Une page HTML simple permettant :
- D’écrire et envoyer des messages
- De voir les messages reçus en temps réel
- Connexion directe au proxy via WebSocket `ws://localhost:8080`
- Pour tester : ouvrir client.html dans un navigateur

