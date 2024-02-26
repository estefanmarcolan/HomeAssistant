# Homeassistant_Remote_Cloudflare

## 1 - Criar uma conta no CloudFlare

## 2 - Conectar o domino (i9smart) 

## 3 - Adicionar Add-on com repositório

3.1 - Configuração
3.2 - Add-ons
3.3 - Loja de ADD-ONS
3.4 - Repositório 

![image](https://github.com/estefanmarcolan/Homeassistant_Remote_Cloudflare/assets/153628041/2a688849-6c3d-44bf-99f3-40a602711e9d)

3.5 - Adicionar repositório
Link do repositorio: ```https://github.com/w35l3y/hassio-addons```

![image](https://github.com/estefanmarcolan/Homeassistant_Remote_Cloudflare/assets/153628041/6aac75c9-508d-421d-8151-053cdd0f8cad)

![image](https://github.com/estefanmarcolan/Homeassistant_Remote_Cloudflare/assets/153628041/edd21103-6a5d-4f04-8a7c-8f70b3ef1c2a)

3.6 - Reiniciar o HA

## 4 - Adicionar Add-on na loja

![image](https://github.com/estefanmarcolan/Homeassistant_Remote_Cloudflare/assets/153628041/f19aa4ad-c343-44ba-a18a-92fabb310cb7)

![image](https://github.com/estefanmarcolan/Homeassistant_Remote_Cloudflare/assets/153628041/dca7e431-cb2f-4b79-b53c-69c7b525262d)

## 5 - Configurando Cloudflare Add-ons no HA

5.1 - Configurar o nome do Túnel, o nome dever ser diferente de qualquer outro túnel, se casso tiver 2 túnel com o mesmo nome, o Cloudflare considera clonado e desconsidera 1.


Em Add-ons com o repositório do CloudFlare instalado, abra o add-ons em '''ajustes''' Defina o nome do túnel e em ingress defina o ```hostname``` Domínio de destino e ```service``` IP do HA.
```yaml
- hostname: ###########.i9smart.com.br
  service: http://################:8123
- service: http_status:404
```


No arquivo '''Configuration.yaml''' adicionar o seguinte código para autorizar o a conexão do CloudFalre com o HA

``` yaml
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 10.0.0.200    
    - 172.30.33.0/24
    - 192.168.0.0/24
```

Configuraçoes no Add-ons feita e salvas, podemos iniciar o Add-ons, em ```log``` o add-ons vai criar o link de certificação, esse link criara o link e coneção do HA no CloudFlare. 

![image](https://github.com/estefanmarcolan/Homeassistant_Remote_Cloudflare/assets/153628041/6d664435-9677-43d1-9741-afb7ded17f24)

![image](https://github.com/estefanmarcolan/Homeassistant_Remote_Cloudflare/assets/153628041/474a86d2-b846-4369-8e74-c7e6963ebc9d)

Confirmando o tunel no add-ons em logs sera gerado um  ``` TunelID ``` esse codigo sera ussado nos DNS em Token.

## 6 - Cloudflare Tunel

Abrir o cloudflare acesse o dominio desejado, em ```DNS``` temos que cria alguns parametros,  ```CNAME``` Segue exemplo: 

| Type          |   Name           | Content |
| ------------- |:----------------:| -------:|
| CNAME         |  Sob Dominio     | Token   |
| CNAME         |  WWW.Sob Dominio | Token   |

No final do token tem que colocar ```.cfargotunnel.com``` 

Confiração CloudFlare Pronta! 

