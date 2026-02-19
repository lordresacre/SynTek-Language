# ⚙️ SYN'TEK: DEVELOPER INTEGRATION GUIDE
**Target Audience:** Game Developers, AI Engineers, Modders.
**Supported Engines:** Unity, Unreal Engine, Godot, Custom Engines.
**Architecture:** Zero-Shot LLM Integration.

## 1. THE CONCEPT: NARRATIVE AS CODE
Traditional game NPCs use predefined dialogue trees. Modern NPCs use LLMs (Large Language Models) to generate dynamic text. 

**Syn'Tek bridges the gap between NPC dialogue and Game Engine execution.**
Because Syn'Tek uses strict semantic tokens and operators (`::`, `>>`, `//`), your game engine can easily parse an NPC's spoken sentence and convert it into executable code (animations, UI updates, combat actions), without needing complex Natural Language Processing (NLP) models.

---

## 2. STEP 1: THE SYSTEM PROMPT (For the NPC's AI)
To make your NPC speak Syn'Tek natively, you do not need to train a custom model (LoRA). You only need to inject the Syn'Tek rules into the LLM's System Prompt.

**Copy/Paste this into your LLM System Prompt:**
```text

You are an NPC in a cyberpunk/sci-fi world.
You communicate EXCLUSIVELY using the Syn'Tek Language protocol.
Rules of Syn'Tek:
1. Syntax: COMMAND :: OBJECT >> DESTINATION !
2. Use absolute tokens: FETCH (get), SPAWN (create), TRAVERSE (move), TRANSFER (give), ABORT (stop).
3. Operators: :: (defines target), >> (defines output/direction), // (parameters).
4. Do not use standard English or French grammar. Be robotic, authoritative, and concise.

Example: If the player asks you for a weapon, reply: "FETCH :: WEAPON [TYPE: RIFLE] >> TARGET: YOU !"

3. STEP 2: PARSING THE OUTPUT (In your Game Engine)
When the LLM generates a Syn'Tek response, display it in the game's dialogue UI so the player can read it.
Simultaneously, run a simple script in your engine (C#, C++, Python) to parse the operators and trigger game events.


Example C# Logic (Unity):

string npcResponse = "FETCH :: RATION [TYPE: PIZZA] >> DEST: HQ";

// 1. Check if it's an actionable Syn'Tek command
if (npcResponse.Contains("::") && npcResponse.Contains(">>")) {
    
    // 2. Parse the Command
    if (npcResponse.StartsWith("FETCH")) {
        // Trigger NPC walking animation towards the item
        TriggerAnimation("WalkAndGrab");
    }
    
    // 3. Parse the Object and Parameters
    if (npcResponse.Contains("[TYPE: PIZZA]")) {
        // Instantiate the specific prefab
        SpawnPrefab("Item_Pizza");
    }
    
    // 4. Parse the Destination
    if (npcResponse.Contains("DEST: HQ")) {
        // Set NPC NavMesh destination to the HQ coordinates
        SetNavTarget(Location.HQ);
    }
}


4. USE CASES FOR GAMEPLAY
Integrating Syn'Tek allows for emergent gameplay mechanics:
Voice Commands: Allow the player to use their microphone to speak Syn'Tek to drones or squadmates. The game's speech-to-text easily translates the strict syntax.
Hacking Minigames: Players must construct correct Syn'Tek syntax chains to bypass security doors (EXEC :: OVERRIDE >> TARGET : DOOR).
Economy & Trading: NPCs process transactions directly via syntax (TRANSFER :: 500 CREDITS >> TARGET : MERCHANT).

5. LEGAL INTEGRATION (MANDATORY)
Syn'Tek is governed by the SCOL v1.0 license.
As a game developer, you are granted automatic, royalty-free permission to use Syn'Tek in your commercial games, under one strict condition:
You must include the following line in your game's end credits or legal documentation:
"Syn'Tek Language Protocol created by Julien Maurel"
Please refer to LICENSE.md (Article 4.6) for full details.
