# Install & Manage Antigravity Hub and IDE on Fedora

## 0. Specs

- OS Fedora KDE 44
- Official Antigravity from Google web, ver 1.107.0

## 1. Initial Installation

1. Download **Antigravity** and **Antigravity IDE** from [Antigravity Google](https://antigravity.google/download).

2. Make install dir in `/opt/` and extract them:
```bash
sudo mkdir -p /opt/antigravity /opt/antigravity-ide

sudo tar -xzf ~/Downloads/Antigravity.tar.gz -C /opt/antigravity --strip-components=1
sudo tar -xzf ~/Downloads/'Antigravity IDE.tar.gz' -C /opt/antigravity-ide --strip-components=1
```

3. Create global sysmlinks: 
```bash
sudo ln -sf /opt/antigravity/antigravity /usr/local/bin/antigravity
sudo ln -sf /opt/antigravity-ide/bin/antigravity-ide /usr/local/bin/antigravity-ide
sudo ln -sf /opt/antigravity-ide/bin/antigravity-ide /usr/local/bin/agy-ide
```

4. Verification, should return version and symlink dir. 
```bash
antigravity-ide --version && which antigravity agy-ide
```

5. Create separate launcher entries:
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

6. Delete the tar downloads to clean the deployment:
```bash
rm -f ~/Downloads/Antigravity.tar.gz ~/Downloads/'Antigravity IDE.tar.gz'
```

## 2. Manage Update

1. Download my [update-Antigravity](https://github.com/CrosshairAWL/PolarbearPC-Install-Docs/blob/main/SCRIPTS/update-Antigravity) bash script. 

2. Chmod +x and run it.

## 3. update-Antigravity Script Bug Report
Please call me at **crosshairawl.ugm@gmail.com** 