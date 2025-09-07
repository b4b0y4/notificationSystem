# Clean Notification System

A lightweight, modern notification system with smooth slide animations. Perfect for displaying toast notifications in web applications.

## Quick Setup

### 1. Add the CSS
Add `notifications.css` to your project or include this in your stylesheet:

```css
:root {
  --color-blue: 75, 186, 231;
  --color-green: 46, 204, 113;
  --color-orange: 255, 165, 0;
  --color-red: 234, 51, 35;
}

#notificationContainer {
  position: fixed;
  bottom: 20px;
  left: 20px;
  z-index: 1000;
  max-width: 400px;
  pointer-events: none;
}

.notification {
  position: relative;
  margin-bottom: 10px;
  transform: translateX(-100%);
  opacity: 0;
  transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  pointer-events: auto;
  max-width: 100%;

  &.show { transform: translateX(0); opacity: 1; }
  &.hide { transform: translateX(-100%); opacity: 0; }

  &.info .notif-content {
    color: rgb(var(--color-blue));
    background-color: rgba(var(--color-blue), 0.1);
    border-left-color: rgb(var(--color-blue));
    box-shadow: 0 8px 32px rgba(var(--color-blue), 0.15);
  }
  &.success .notif-content {
    color: rgb(var(--color-green));
    background-color: rgba(var(--color-green), 0.1);
    border-left-color: rgb(var(--color-green));
    box-shadow: 0 8px 32px rgba(var(--color-green), 0.15);
  }
  &.warning .notif-content {
    color: rgb(var(--color-orange));
    background-color: rgba(var(--color-orange), 0.1);
    border-left-color: rgb(var(--color-orange));
    box-shadow: 0 8px 32px rgba(var(--color-orange), 0.15);
  }
  &.danger .notif-content {
    color: rgb(var(--color-red));
    background-color: rgba(var(--color-red), 0.1);
    border-left-color: rgb(var(--color-red));
    box-shadow: 0 8px 32px rgba(var(--color-red), 0.15);
  }
}

.notif-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 20px;
  border-radius: 8px;
  font-size: 15px;
  font-weight: 500;
  backdrop-filter: blur(10px);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.12);
  border-left: 4px solid;
  position: relative;
  overflow: hidden;
}

.notif-message { display: flex; align-items: center; gap: 12px; flex: 1; }

.notif-close {
  background: none; border: none; font-size: 20px; cursor: pointer;
  width: 24px; height: 24px; display: flex; align-items: center;
  justify-content: center; margin-left: 12px; color: currentColor;
}

.progress-bar {
  position: absolute; bottom: 0; left: 0; right: 0; height: 3px;
  background-color: currentColor; opacity: 0.6; transform-origin: left;
  animation: progress linear;
}

@keyframes progress {
  from { transform: scaleX(1); }
  to { transform: scaleX(0); }
}

@media (max-width: 480px) {
  #notificationContainer { left: 10px; right: 10px; bottom: 10px; max-width: none; }
  .notif-content { padding: 12px 16px; font-size: 14px; }
}
```

### 2. Add the HTML Container
```html
<div id="notificationContainer"></div>
```

### 3. Add the JavaScript Module
Import the `NotificationSystem` class into your JavaScript file:

```javascript
import NotificationSystem from './notifications.js';
````

## Usage

### Basic Notifications
```javascript
NotificationSystem.show('Operation completed!', 'success');
NotificationSystem.show('Please check your input', 'warning');
NotificationSystem.show('Something went wrong!', 'danger');
NotificationSystem.show('Here is some information', 'info');
```

### With Options
```javascript
// Persistent notification (won't auto-hide)
NotificationSystem.show('Important message', 'info', { duration: 0 });

// Custom duration (7 seconds)
NotificationSystem.show('Custom timing', 'success', { duration: 7000 });

// No close button or progress bar
NotificationSystem.show('Clean message', 'warning', {
  closable: false,
  showProgress: false
});
```

## Options

| Option | Default | Description |
|--------|---------|-------------|
| `duration` | `5000` | Auto-hide delay in ms (0 = persistent) |
| `closable` | `true` | Show close button |
| `showProgress` | `true` | Show progress bar |
| `html` | `false` | Allow HTML content |
