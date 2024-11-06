{
  "format_version": 2,
  "header": {
    "description": "My Custom Minecraft Add-On",
    "name": "My Custom Add-On",
    "uuid": "1d6b58ad-8462-4d47-b6fa-2cbd2a8c20e5", 
    "version": [1, 0, 0]
  },
  "modules": [{
    "description": "My Custom Scripts",
    "entry": "scripts/main.js",
    "uuid": "4bba4d3e-47bb-4057-8201-d0b9bde56eac",
    "version": [1, 0, 0],
    "type": "scripting"
  }],
  "dependencies": []
}
// main.js
let system = server.registerSystem(0, 0);

system.initialize = function() {
    this.listenForEvent("minecraft:item_use", (eventData) => this.onItemUse(eventData));
};

system.onItemUse = function(eventData) {
    let player = eventData.data.player;
    let itemStack = eventData.data.item_stack;

    // Check if the player used the custom item (example: diamond sword with a custom name)
    if (itemStack.id === "minecraft:diamond_sword" && itemStack.name === "My Special Sword") {
        // Perform some action, e.g., give the player a message
        this.broadcastMessage(player.name + " used the special sword!");
        
        // You could add custom logic here (e.g., teleporting, spawning entities, etc.)
    }
};

// Utility to broadcast messages to the player
system.broadcastMessage = function(message) {
    this.broadcastEvent("minecraft:display_chat_event", message);
};
