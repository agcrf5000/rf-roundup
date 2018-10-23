IPC

Electron
const electron = require('electron');
const { ipcMain } = electron;
Listen: ipcMain.on('[category]:[action]', (event, [data]) => {})
Send: mainWindow.webContents.send('[category]:[action]', [data]);

BrowserWindow
const electron = require('electron');
const { ipcRenderer } = electron;
Send: ipcRenderer.send('[category]:[action]', [data]);
Listen: ipcRenderer.on('[category]:[action]', (err, [data]) => {})
