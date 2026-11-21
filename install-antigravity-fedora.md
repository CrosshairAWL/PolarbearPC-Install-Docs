# Install Antigravity app and IDE on Fedora

## 0. Specs

- OS Fedora KDE 44
- Official Antigravity from Google web, ver 1.107.0

## 1. Installation

1. Download **Antigravity** and **Antigravity IDE** from [Antigravity Google](https://antigravity.google/download)

2. Rename them to `Antigravity.tar.gz` and `Antigravity_IDE.tar.gz` (for convenient installation).

3. Make install dir in `/opt/` and extract them:
```bash
sudo mkdir -p /opt/antigravity /opt/antigravity-ide

sudo tar -xzf ~/Downloads/Antigravity.tar.gz -C /opt/antigravity --strip-components=1
sudo tar -xzf ~/Downloads/Antigravity_IDE.tar.gz -C /opt/antigravity-ide --strip-components=1
```

4. Create global sysmlinks: 
```bash
sudo ln -sf /opt/antigravity/antigravity /usr/local/bin/antigravity
sudo ln -sf /opt/antigravity-ide/bin/antigravity-ide /usr/local/bin/antigravity-ide
sudo ln -sf /opt/antigravity-ide/bin/antigravity-ide /usr/local/bin/agy-ide
```

5. Verification, should return version and symlink dir. 
```bash
antigravity-ide --version && which antigravity agy-ide
```

6. Create separate launcher entries:
```bash
IDE_ICON=$(find /opt/antigravity-ide -name "code.png" -o -name "*antigravity*.png" | head -n 1)

cat << 'EOF' | sudo tee /usr/share/applications/antigravity.desktop > /dev/null
[Desktop Entry]
Name=Antigravity
Comment=Google Antigravity Agent Hub
Exec=/usr/local/bin/antigravity --ozone-platform-hint=auto %U
Icon=applications-development
Type=Application
StartupNotify=true
StartupWMClass=Antigravity
Categories=Development;IDE;
EOF

cat << EOF | sudo tee /usr/share/applications/antigravity-ide.desktop > /dev/null
[Desktop Entry]
Name=Antigravity IDE
Comment=Agentic Code Editor powered by Gemini
Exec=/usr/local/bin/antigravity-ide --ozone-platform-hint=auto %F
Icon=${IDE_ICON:-applications-development}
Type=Application
StartupNotify=true
StartupWMClass=Antigravity IDE
Categories=Development;IDE;
MimeType=text/plain;inode/directory;
EOF

sudo update-desktop-database /usr/share/applications
```