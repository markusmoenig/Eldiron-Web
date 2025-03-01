---
title: Examples
description: "Scripting Examples"
---

## Opening a Door

Opening a door can be achieved in different ways depending on your **gameplay mechanics**. For example, you could open a door when:
- A character **bumps into it**.
- The player **clicks a "Use" or "Open" button**.

Let's start with the **simplest approach**: opening a door when a character **bumps into it**.

### **Example: Auto-Opening Door**

```python
# Taken from https://github.com/markusmoenig/Eldiron/blob/master/examples/Harbor.eldiron

class Door:

    def event(self, event, value):

        if event == "bumped_by_entity":
            set_attr("visible", False)
            set_attr("blocking", False)
            notify_in(2, "close_door")

        if event == "close_door":
            if len(entities_in_radius()) == 0:
                set_attr("visible", True)
                set_attr("blocking", True)
            else:
                notify_in(2, "close_door")
```

### **How It Works**
1. When a character **bumps into the door**, the `bumped_by_entity` event is triggered.
2. The door **opens** by setting:
   - `visible = False` (door disappears).
   - `blocking = False` (door no longer blocks movement).
3. The `notify_in(2, "close_door")` function **delays closing** the door for **2 seconds**.
4. When `close_door` is triggered, the script:
   - **Checks if the area is empty** (`entities_in_radius() == 0`).
   - If **empty**, the door **closes** (`visible = True`, `blocking = True`).
   - If **not empty**, it **delays the closing** again by 2 seconds.

> [!NOTE]
> Setting the `blocking` attribute isn’t strictly necessary in this case, since the door **instantly opens** on contact. However, it is included here for **clarity and flexibility** in different scenarios.
