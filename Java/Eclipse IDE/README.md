# Eclipse IDE

[link do eclipse](https://www.eclipse.org/downloads/packages/release)

- Baixa o eclipse.

- Extrai o arquivo

- Cria o app

```
touch ~/.local/share/applications/Eclipse.desktop
```

- Abre o editor de texto

```
gedit ~/.local/share/applications/Eclipse.desktop
```

- Cola isso e ajeita né

```
[Desktop Entry]
Comment=Eclipse
Terminal=false
Name=Eclipse
Exec=/caminho/para/versao/eclipse/eclipse
Type=Application
Icon=/caminho/para/icone/eclipse/icon.xpm
StartupWMClass=Eclipse
```

- Exemplo na pasta home pwd

```
[Desktop Entry]
Comment=Eclipse
Terminal=false
Name=Eclipse
Exec=/home/elros/eclipse-jee-2023-06-M2-linux-gtk-x86_64/eclipse/eclipse
Type=Application
Icon=/home/elros/eclipse-jee-2023-06-M2-linux-gtk-x86_64/eclipse/icon.xpm
StartupWMClass=Eclipse
```

- Transformar em um app

```
chmod a+x ~/.local/share/applications/Eclipse.desktop

```
