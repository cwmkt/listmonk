<p align="center">
<img src="https://cwmkt.com.br/wp-content/uploads/2023/08/logo-github-cwmkt.svg" alt="DispZap Whats Marketing" width="240" />
<p align="center">Seja bem-vindo ao Guia de Instalação listmonk 🚀</p>
</p>
  
<p align="center">
<img src="https://whatsapp.com/favicon.ico" alt="WhatsAPP-logo" width="32" />
<span>Grupo WhatsaAPP: </span>
<a href="https://link.cwmkt.com.br/quepasa" target="_blank">Grupo</a>
</p>

<hr />

<img src="https://github.com/cwmkt/listmonk/assets/34479816/2432e65f-71c2-465b-9498-df7e30e6c1c7" alt="WhatsAPP-logo" />

**listmonk** is a self-hosted, high performance mailing list and newsletter manager. It comes as a standalone binary and the only dependency is a Postgres database.

### Atualize os pacotes de sua máquina

```bash
sudo apt update && apt upgrade -y
```

### Instale o Docker-compose V2

```bash
sudo apt-get install docker-compose-v2
```

### Inicie a instalação do listmonk com script abaixo

```bash
mkdir listmonk && cd listmonk
bash -c "$(curl -fsSL https://raw.githubusercontent.com/knadh/listmonk/master/install-prod.sh)"
```

### Agora vamos instalar o nginx para criar o proxy reverso

```bash
sudo apt install nginx
```

```bash
sudo nano /etc/nginx/sites-available/listmonk
```

```bash
server {
  server_name mailersend.seudominio.com.br;
  
  underscores_in_headers on;

  location / {

   proxy_pass http://127.0.0.1:9000;
   proxy_pass_header Authorization;
   proxy_set_header Upgrade $http_upgrade;
   proxy_set_header Connection "upgrade";
   proxy_set_header Host $host;
   proxy_set_header X-Forwarded-Proto $scheme;
   proxy_set_header X-Forwarded-Ssl on; # Optional
   proxy_set_header X-Real-IP $remote_addr;
   proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
   proxy_http_version 1.1;
   proxy_set_header Connection "";
   proxy_buffering off;
   client_max_body_size 0;
   proxy_read_timeout 36000s;
   proxy_redirect off;
  }
  add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
  ssl_protocols TLSv1.2 TLSv1.3;
}
```

```bash
sudo ln -s /etc/nginx/sites-available/listmonk /etc/nginx/sites-enabled
```

```bash
sudo apt-get install snapd -y
```

```bash
sudo snap install notes
```

```bash
sudo snap install --classic certbot
```

```bash
sudo certbot --nginx
```

```bash
sudo service nginx restart
```

### Pronto ✅ Instalação concluída
Para acessar basta acessar seudominio.com.br</br>
Os dados de acesso padrão estão no arquivo `config.toml` que está localizado em /root/listmonk

