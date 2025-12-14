---
title: Among Us Game Hacking Guide
published: 2025-12-14
description: A simple guide to showing you how to implement some features in Among Us
tags: [Game Hacking, Reverse Engine]
category: Game Hacking
draft: false
---

# Among Us Game Hacking Guide
#### Tools: MelonLoader (Mod loader), Untiy Explorer (Mod)

### Speed hack:
```
scene -> localPlayerName(object) -> Il2Cpp.PlayerPhysics(Components) -> PlayerPhysics.Speed = 12.5 (float)
```

### Sabotage without impostor role:
you need to manually open map at least once, else you would not see the ShipMap(Clone) object.
```
scene -> Main Camera(object) -> Hud(object) -> ShipMap(Clone) -> InfectedOverlay(object).Activate = True
```

### Noclip hack:
```
scene -> playerName(object) -> UnityEngine.CircleCollider2D(Components).Activate = False
```

### Remove shadow / Fullbright:
```
scene -> Main Camera(object) -> ShadowQuad(object).Activate = False
```

### Force show chat button:
```
scene -> Main Camera(object) -> ChatUi(object).Activate = True
```

### Manipulation position / Teleport hack
```
scene -> localPlayerName(object).Position = {0,0,0} (Vector3 X,Y,Z)
```
