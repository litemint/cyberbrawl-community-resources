# Cyberbrawl API Documentation

Base URL: `https://connect.cyberbrawl.io`

---

## Library
Get the list of all cards currently available in the game.

**URL**: `https://connect.cyberbrawl.io/library`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "card_01_00001": {
    "id": "card_01_00001",
    "type": 1,
    "name": "Overload I",
    "stats": [2, 0, 0, 0],
    "boost": 0,
    "desc": ""
  },
  "card_02_00012": {
    "id": "card_02_00012",
    "type": 2,
    "name": "Card Name",
    "stats": [0, 4, 0, 0],
    "boost": 0,
    "desc": "Card description"
  }
}
```

---

## Player
Get player profile and stats

**URL**: `https://connect.cyberbrawl.io/player?id={playerId}`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "id": "kyungjin",
  "name": "Kyungjin",
  "back": 8,
  "stats": [125, 1323800, 64, 0, 29, 5428, 7869, 60],
  "badges": {
    "legend": true,
    "elite": false,
    "dev": true
  }
}
```

---

## Leaderboard
Get leaderboard rankings.

**URL**: `https://connect.cyberbrawl.io/server/leaderboard?name={name}`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
[
  {
    "id": "ihgux3",
    "name": "Pipay",
    "back": 10,
    "stats": [125, 1246575, 59, 2, 56, 30685, 40002, 11520],
    "score": 4194
  }
]
```

---

## Server Stats
Get overall game statistics.

**URL**: `https://connect.cyberbrawl.io/server/stats`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "credit": {
    "supply": 299792458,
    "earned": 22070571.68711
  },
  "players": {
    "total": 160567
  },
  "battles": {
    "total": 6287446
  }
}
```

---

## Battle Replays
Get recent battle replay data.

**URL**: `https://connect.cyberbrawl.io/battles/replay`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "result": [
    {
      "id": "p87ajw",
      "turns": 10,
      "players": [
        {"name": "Jieun", "id": "jieun", "winner": true},
        {"name": "Kyungjin", "id": "kyungjin", "winner": false}
      ]
    }
  ]
}
```

---

## Badges
Get the list of available player badges.

**URL**: `https://connect.cyberbrawl.io/badges`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
[
  {"id": 0, "name": "Trailblazer", "property": "trailblazer"},
  {"id": 1, "name": "Champion", "property": "elite"},
  {"id": 2, "name": "Legend", "property": "legend"}
]
```

---

## Heroes
Get the list of available heroes.

**URL**: `https://connect.cyberbrawl.io/heroes`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
[
  {"id": 0, "name": "Arya", "property": "arya"}
]
```

---

## Card Backs
Get the list of available card backs.

**URL**: `https://connect.cyberbrawl.io/cardbacks`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
[
  {"id": 0, "name": "Cyber Brawl", "desc": "Cyber Brawl Logo"},
  {"id": 1, "name": "Red Dragon", "desc": "By Prasong Tadoungsorn"},
  {"id": 5, "name": "Insignia", "desc": "Show off your rank!"}
]
```

---

## Community
Get community content and featured videos.

**URL**: `https://connect.cyberbrawl.io/server/community`  
**Method**: `GET`  
**Auth required**: No

### Success Response
**Code**: `200 OK`

**Content example**:
```json
{
  "links": [
    {
      "id": "link-eb34e83d-wow1-0",
      "author": "Fred Kyung-jin Rezeau",
      "desc": "CyberBrawl Dev",
      "link": "https://www.youtube.com/watch?v=xLkj-wEfvsg",
      "image": "https://img.youtube.com/vi/xLkj-wEfvsg/hqdefault.jpg"
    }
  ]
}
```
