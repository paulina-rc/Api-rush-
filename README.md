# API Rush

A live multiplayer quiz game about APIs, made for a 40-minute Technical English class (11th grade, Work Guide #6 “Teach to Learn”). The teacher runs the game on the projector, and every student plays from their own phone.

**Play:** https://paulina-rc.github.io/Api-rush-/
**Teacher screen:** https://paulina-rc.github.io/Api-rush-/?host

## How it works

1. The teacher opens the link with `?host` on the classroom computer. A QR code and a 4-digit game code appear on the screen.
2. Students scan the QR code (or open the link and type the code), then type their name.
3. Each challenge works like a request to a server. Players have 20 seconds to answer A, B, C or D on their phone.
4. The faster the answer, the more points it earns: up to 1,000 points per challenge.
5. After each challenge, the board shows how the class answered and the top 5 players.

Results on the phone use real HTTP status codes:

| Code | Meaning in the game |
| --- | --- |
| `200 OK` | Correct answer |
| `400 Bad Request` | Wrong answer |
| `408 Timeout` | No answer before the timer ended |
| `202 Accepted` | Answer received, waiting for the result |

## Rounds

| Round | Topic | Points |
| --- | --- | --- |
| 1 · Who am I? | Key vocabulary: server, API key, endpoint | Normal |
| 2 · Pick the method | HTTP methods: GET, POST, PUT | Normal |
| 3 · Read the JSON | Keys and values in a JSON response | Normal |
| Final round | Status codes, DELETE, the restaurant analogy | Double |

## Surprise server events

Three events appear during the game, in random order:

- **2× BONUS:** the next challenge is worth double points for everyone.
- **429 RATE LIMIT:** the player in first place can’t score on the next challenge.
- **201 CREATED:** the three players in last place get +300 points.

## Presenter controls

| Key | Action |
| --- | --- |
| `Space` | Reveal the answer before the timer ends |
| `N` | Next challenge / continue after an event |

The answer is also revealed automatically when every player has answered or when the time runs out.

## Tech

- One self-contained `index.html`: HTML, CSS and vanilla JavaScript, hosted on GitHub Pages.
- Real-time communication with [MQTT.js](https://github.com/mqttjs/MQTT.js) over WebSockets, using a free public broker (`broker.emqx.io`, with `broker.hivemq.com` as backup). No accounts, keys or backend needed.
- The teacher’s screen is the game server: it publishes the game state, and the phones send their answers.
- QR code generated with [qrcode.js](https://github.com/davidshimjs/qrcodejs).

## Troubleshooting

If the screen says **“Can’t reach the game server”**, the network is probably blocking the connection to the broker. Connect the computer to a phone hotspot, and ask students to use mobile data instead of the school Wi-Fi.

## Credits

Made by Paulina R. ([PR.DEV](https://github.com/paulina-rc)) for the Technical English final project at Colegio Agropecuario de San Carlos, 2026.
