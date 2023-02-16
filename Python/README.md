# Python

1. Instale o python

```
sudo apt install python3
```

## pyenv

2. Baixe e instale o pyenv

```
curl https://pyenv.run | bash
```

3. Reinicie seu shell para que as mudanças tenham efeito

```
exec $SHELL
```

4. Você precisará acessar o arquivo .bashrc (ou .zshrc, se você usa zsh/ohmyzsh) para adicionar algumas linhas.

- Para abrir o arquivo no local ~/.bashrc use o nano ou algum outro editor de arquivos

```
nano ~/.bashrc
```

- Certifique-se de que as seguintes linhas estão no seu arquivo de configuração .bashrc e, caso não estejam, faça a inclusão no final do arquivo

```
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init --path)"
fi
```

5. Abra um novo terminal e execute o comando para verificar a instalação:

```
pyenv
>
```

### como usar

- Para listar tudo que se pode instalar com o pyenv, faça:

```
pyenv install -l
```

- Instale uma versão do Python, por exemplo, 3.9.1

```
pyenv install 3.9.1
```

- Faça com que a versão que você acabou de instalar, seja a versão global de seu sistema

```
pyenv global 3.9.1
```

## Pip

instale o pip

```
sudo apt install python3-pip
```

verifique se tá tudo certo

```
python3 -m pip --version
```

A saída deverá ser similar a apresentada abaixo:

```
pip 19.2.3 from /usr/lib/python3.8/site-packages (python 3.8)
```

## Venv

- instale

```
sudo apt install python3-venv
```

- verifique

```
python3 -m venv -h
```

## Flake8

- instale

```
sudo python3 -m pip install flake8
```

- verifique

```
python3 -m flake8 --version
```

deverá parecer isso aqui

```
3.8.4 (mccabe: 0.6.1, pycodestyle: 2.6.0, pyflakes: 2.2.0)
```

## Black

- instale

```
sudo python3 -m pip install black
```

- verifique

```
python3 -m black --version
```

deverá aparecer isso aqui

```
__main__.py, version 20.8b1
```

## VSCode(python)

- instale a extensão do python no vs code

- Após instalar a extensão, digite ctrl + shift + p, vá em Preferences: Open Settings (JSON) e acrescente as seguintes configurações.

```
// ...
    "python.linting.enabled": true,
    "python.linting.flake8Enabled": true,
    "python.formatting.blackArgs": [
        "-l 79"
    ],
    "python.formatting.provider": "black",
// ...
```

## CodeRunner

CodeRunner normal no vsCode

add isso nas settings

```
// ...

    "code-runner.executorMap": {
        "python": "python3 -u"
    },
    "code-runner.runInTerminal": true,

// ...
```
