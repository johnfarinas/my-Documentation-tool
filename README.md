# Multi-Session Incident Documentation Tool

**(Stable / Dark Mode Default)**  **Type:** Client-Side Single Page Application (SPA)

* * *

### **Executive Overview**

This is a lightweight, offline-first documentation engine designed for IT professionals, Service Desk Analysts, and Sysadmins. It allows users to track multiple concurrent incidents, generate real-time timestamps, manage screenshots, and export structured data without needing a database or internet connection.

### **Core Interface & Layout**

The interface is engineered for high-density information display using a fixed vertical split:

- **10% - Incident Header:** Compact, flex-wrap grid for high-level ticket data (Caller, SDP, Incident ID).
    
- **50% - Tactical Timeline:** The primary workspace. A scrollable table for logging actions and results.
    
- **40% - "My Notes" Preview:** A real-time, auto-generated summary formatted for email or ticket updates.
    
- **Sticky Footer:** A non-overlapping control bar for file operations and theming.
    

### **Multi-Session Capabilities**

- **Tabbed Interface:** Just like a web browser, you can open multiple unique sessions (tabs) to handle concurrent tickets (e.g., one tab for a network outage, another for a password reset).
    
- **Auto-Naming:** Tabs automatically rename themselves based on the "SDP" (Service Desk Ticket) field input.
    
- **State Persistence:** If you close the browser, all open tabs and their data are saved in `localStorage` and restored upon reopening.
    
- **Safety Lock:** Clicking "Close (X)" on a tab triggers a confirmation prompt asking if you want to save your work before the session is destroyed.
    

### **The Timeline (The Engine)**

- **F5 Hotkey:** Pressing `F5` instantly inserts a new row with the current system time.
    
- **Smart Timestamps:** Time is auto-generated but fully editable.
    
- **Rich Media Support:** You can paste screenshots (Ctrl+V) directly into table cells.
    
- **Image Management:**
    
    - Images render as thumbnails.
        
    - **Lightbox:** Clicking a thumbnail opens it full-screen for review.
        
    - **Delete Button:** A dedicated "X" button on the thumbnail removes the image.
        
- **3D Delete Logic:** To prevent accidental deletion of logs, the row delete button uses a **"3-Second Arming"** mechanism. You must click once to "Arm" (it counts down 3..2..1) and click again to confirm deletion.
    

### **File System & Data Export**

- **File System Access API:** The tool integrates directly with the OS file explorer.
    
- **Set Root Folder:** Users select a folder on their computer once. All subsequent saves go directly to that folder (no more "Downloads" folder clutter).
    
- **Dual-Stream Saving:**
    
    - **JSON:** Saves the full state (text + images) to be re-opened later.
        
    - **TXT:** Exports a clean, plain-text version of the notes for pasting into ticketing systems.
        
    - **Image Extraction:** When saving, the tool loops through the timeline, extracts all pasted screenshots, and saves them as individual `.png` files in the root folder alongside the logs.
        

### **"My Notes" Auto-Generator**

- **Real-Time Formatting:** As you type in the timeline, the "My Notes" section at the bottom automatically formats the data into a readable narrative:
    
    - **Header:** Caller / SDP / Incident / Subject.
        
    - **Body:** Description.
        
    - **Log:** A chronological list of `Time: Action -> Result`.
        
- **One-Click Copy:** A "Copy" button places the formatted HTML/Text into the clipboard, ready to paste into Outlook or ServiceNow.
    

### **UI/UX Features**

- **Default Dark Mode:** Designed to reduce eye strain during long shifts. High-contrast text on slate backgrounds.
    
- **Visual Polishing:**
    
    - Tabs mimic physical folders with a "pop-up" active state.
        
    - Action buttons use 3D styling with "press" physics.
        
    - Inputs use a 14px font for clear legibility.
        
- **Responsive Design:** The layout uses Flexbox to ensure the sticky footer never overlaps the content, and scrollbars appear only where needed.
    

* * *

User Workflow**

1.  **Start:** Open the HTML file. It loads in Dark Mode with a fresh session.
    
2.  **Log:** Type the Caller and Incident ID.
    
3.  **Action:** Press `F5`. Type "Ping server" in Action, "No response" in Result.
    
4.  **Evidence:** Take a screenshot of the ping failure. Click the Timeline cell. Press `Ctrl+V`. The image appears.
    
5.  **Multi-Task:** Click `+ New Session`. A new tab opens for a second incoming call.
    
6.  **Save:** Click "Set Root Folder" -> Select `C:\Incidents`. Click "Save JSON".
    
    - *Result:* `INC_12345.json` and `INC_12345_img_0.png` are saved to `C:\Incidents`.
7.  **Finish:** Click "Copy" and paste the summary into the official ticket. Click the "X" on the tab to close.
