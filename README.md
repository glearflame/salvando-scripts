# LW Hacking OS

Configuração de uma distribuição Linux baseada em Debian, montada com
[live-build](https://wiki.debian.org/Repositories/LiveBuild). Gera uma ISO
com XFCE, instalador Calamares e um conjunto de ferramentas de linha de
comando próprias.

Não é um fork de distro: é a **receita** de build. O Debian continua sendo o
Debian — o que muda é o que vem instalado, o branding e os utilitários.

## Estrutura

```
minha-distro/
└── config/
    ├── package-lists/            # o que entra na ISO
    ├── includes.chroot/          # arquivos copiados para dentro do sistema
    │   ├── usr/local/bin/lw              # CLI principal
    │   ├── usr/local/bin/lw-tools        # gerenciador de ferramentas
    │   ├── usr/local/bin/lw-hardware-detect
    │   ├── usr/local/bin/lw-performance
    │   ├── usr/local/bin/lw-dashboard
    │   ├── usr/local/bin/lw-postinstall
    │   ├── etc/calamares/branding/lw     # branding do instalador
    │   └── etc/skel/                     # perfil padrão de usuário novo
    ├── bootloaders/grub/         # tema do GRUB
    └── hooks/normal/             # hooks executados no fim do build
```

Os utilitários `lw*` são `sh` puro e leem identidade de
`/usr/share/lw/identity.env` (`LW_NAME`, `LW_VERSION`, `LW_DESCRIPTION`), então
o branding fica em um arquivo só.

## Build

Precisa de Debian/Ubuntu com `live-build` instalado e root.

```sh
sudo apt install live-build
cd minha-distro
sudo lb build
```

A ISO sai no diretório de trabalho. Build de live-build é demorado na primeira
vez (baixa e descompacta o sistema base).

> `lb clean` antes de rebuildar depois de mexer em `package-lists/` ou
> `includes.chroot/`.

## Status

Projeto experimental, sem releases publicadas. Se você quer só um Linux com
ferramentas de segurança, Kali ou Parrot resolvem com muito menos trabalho —
este repositório é sobre aprender como uma distro é montada por dentro.

Licença MIT.
