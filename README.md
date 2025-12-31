# Home Assistant Media Remote

This is a mobile-friendly remote dashboard for Home Assistant, designed for use on personal devices like phones or tablets. It allows multiple users in different rooms to control their local media and lighting independently.

## 🎯 Features

- **Room-specific media controls**: Users see controls for the room they are in.
- **Lighting status panels**: Show the current state of lights in key areas.
- **Room presence toggles**: `input_boolean.using_<room>` entities track whether a room is actively being used and can disable automations like motion-activated lights.
- **Modular structure**: UI components are broken into reusable YAML blocks under `remote/`.

## 📁 Files Included

- `view_Remote.yaml`: main dashboard view
- `view_Family_Room.yaml` and `view_Media_Room.yaml`: room-specific views
- `remote/`: includes UI blocks like:
  - `block_using_rooms.yaml`
  - `block_media.yaml`
  - `block_lights.yaml`
  - etc.

## 🛠️ Setup Instructions

To adapt this to your own Home Assistant setup:

1. **Copy the files** into your `views/` or `dashboards/` directory.
2. **Update entity IDs**:
   - Replace `light.` and `media_player.` entities with your own devices.
   - Adjust `input_boolean.using_<room>` booleans to match your room names.
3. **Create room selection scripts**:
   - These control what media view is shown. For example:
     ```yaml
     script:
       remote_set_media_room:
         alias: Set Remote to Media Room
         sequence:
           - service: input_select.select_option
             target:
               entity_id: input_select.remote_room
             data:
               option: "Media Room"
     ```
     Create similar scripts for other rooms (`Family Room`, etc.).
4. **Configure the presence logic**:
   - You may want to automate toggling `input_boolean.using_<room>` based on motion or device presence.

## 💡 How It Works

- The remote checks which room is selected via an `input_select` like `input_select.remote_room`.
- Based on this selection, it dynamically loads the correct room view using `state-switch`.
- Presence booleans let users disable automations (like auto-off lights) while they’re manually using the room.

## 📱 Designed For

This UI was designed primarily for **mobile phones**, allowing quick access to room-specific controls in a clean, friendly layout.

---

You’re free to fork, adapt, and remix this for your own smart home.
