# configuracao-NGINX-Ubuntu


#  sudo apt-get update
#  sudo apt-get upgrade

# Instalando e configurando o Nginx
1) sudo apt-get install nginx
2) sudo service nginx start

----------------------------
cd /etc/nginx/sites-available

# Com as duas pastas criadas, precisamos abrir o arquivo de configuração geral do Nginx:
sudo vi /etc/nginx/nginx.conf

# Agora basta adicionar uma linha dentro do bloco http { }:
3) include /etc/nginx/sites-enabled/*;

----------------------------
cd /etc/nginx/sites-available

4) sudo vi nome_do_projeto
# modelo de script para configurar endereços de requisições: IP e hostname

5) --->
server {
    server_name meudominio.com.br www.meudominio.com.br;    

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header X-Forwarded-Host $server_name;
        proxy_set_header X-Real-IP $remote_addr;
	  proxy_read_timeout 360000;
        proxy_connect_timeout 360000;
        proxy_send_timeout 360000;
        add_header P3P 'CP="ALL DSP COR PSAa PSDa OUR NOR ONL UNI COM NAV"';
    }
}

----------------------------

############# checagem de script --> sudo nginx -t

cd /etc/nginx/sites-enabled

6) sudo ln -s /etc/nginx/sites-available/nome_do_projeto
7) sudo rm default
8) sudo service nginx restart

# VERIFICAR NECESSIDADE --->> INSTALAÇÃO MYSQL
sudo apt-get install python3-dev default-libmysqlclient-dev build-essential
