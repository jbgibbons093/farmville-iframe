# Hughberry Farms - Portals Iframe Controller

Master controller and UI iframes for Hughberry Farms, a Farmville-style farming game in Portals.

## Live URL

```
https://jbgibbons093.github.io/farmville-iframe/
```

## Iframes

| File | Purpose | URL |
|------|---------|-----|
| `index.html` | Main game controller & HUD | `/index.html` |
| `seed-store.html` | Buy seeds (6 types) | `/seed-store.html` |
| `sell-goods.html` | Sell crops, products, crafted items | `/sell-goods.html` |
| `crafting.html` | Craft items (requires recipes) | `/crafting.html` |
| `blueprints-store.html` | Buy equipment & recipes | `/blueprints-store.html` |
| `decorations-store.html` | Coming soon placeholder | `/decorations-store.html` |

## Game Features

### Seed Store
- 6 crop types: Wheat, Carrot, Corn, Potato, Tomato, Pumpkin
- Level-gated unlocks (Lv1-5)
- Buy 1 or 5 at a time

### Sell Goods
- **Crops Tab**: Sell harvested crops
- **Products Tab**: Sell animal products (Milk, Wool, Eggs, etc.)
- **Crafted Tab**: Sell crafted items for premium prices

### Crafting System
- 11 recipes available
- **Requires purchasing recipe blueprint first**
- No gold cost to craft (only ingredients consumed)
- Recipes show locked state until purchased

### Blueprint Store
**Equipment:**
- Harvest Basket (200g, Level 2) - Required for egg collection
- Bee Suit (400g, Level 3) - Required for honey collection

**Recipes (11 total):**
- Flour Recipe (100g, Lv1)
- Butter Recipe (150g, Lv2)
- Cheese Recipe (200g, Lv2)
- Bread Recipe (250g, Lv2)
- Blanket Recipe (250g, Lv3)
- Stew Recipe (300g, Lv3)
- Ragout Recipe (400g, Lv4)
- Pie Recipe (400g, Lv4)
- Mead Recipe (450g, Lv4)
- Meat Pie Recipe (500g, Lv5)
- Cake Recipe (600g, Lv5)

## Portals Integration

### SDK Setup Pattern
All iframes use the retry-based SDK initialization:

```javascript
function setupMessageListener() {
  if (typeof PortalsSdk !== 'undefined' && PortalsSdk.setMessageListener) {
    PortalsSdk.setMessageListener(handleMessage);
  } else {
    setTimeout(setupMessageListener, 100);
  }
}

// Fallback postMessage listener
window.addEventListener('message', function(event) {
  if (event.data && event.data.portalsMessage) {
    handleMessage(event.data.portalsMessage);
  }
});

// Request sync on load
setTimeout(() => triggerTask('Sync_Inventory'), 500);
```

### Message Protocol

**From Portals to Iframe:**
```
Sync_Inventory_Gold_100_XP_50_Level_3_Seeds_Wheat_10_...
```

**From Iframe to Portals:**
```javascript
PortalsSdk.sendMessageToUnity(JSON.stringify({
  TaskName: 'Buy_Seeds_Wheat_5',
  TaskTargetState: 'SetNotActiveToActive'
}));
```

## Development

### Testing with Cache Busters
```
https://jbgibbons093.github.io/farmville-iframe/index.html?v=20260125b
```

### Local Development
1. Edit HTML files
2. Commit and push to GitHub
3. Wait ~1 min for GitHub Pages deployment
4. Test in Portals with cache buster URL

## License

MIT
