## instagram-webscraping

<p align="center">
<a href="https://github.com/SeleniumHQ/selenium">
<img src="https://img.shields.io/badge/built%20with-Selenium-yellow.svg" />
</a>
<a href="https://www.python.org/">
<img src="https://img.shields.io/badge/built%20with-Python3-red.svg" />
</a>
<p/>


<p align="center">

## Objetivo
Este tutorial visa dar uma visão simplista da biblioteca selenium, para agilizar o aprendizado de novos usuários nos estudos da mesma. Neste tutorial iremos usar o Anaconda como ambiente para desenvolvimento.

## O que é o selenium
O Selenium é uma lib que permite definir testes e detectar automaticamente os resultados desses testes em um navegador preferido. Um conjunto de funções do Selenium possibilita criar interações passo a passo com uma página da web, simulando um usuário normal do sistema.
<a href='https://www.browserstack.com/guide/python-selenium-to-run-web-automation-test'>[1]<a/>

## 💿Como instalar
Para instalar o Selenium basta executar desse modo a biblioteca será baixada para o seu ambiente Anaconda: <br>
```sh
[1] pip install selenium
```

## Imports necessários
```sh
# Espera algo
from selenium.webdriver.support.ui import WebDriverWait
# Configurações da página web
from selenium.webdriver.firefox.options import Options
# Envia comandos do teclado (enter, f1, f2,...,f12)
from selenium.webdriver.common.keys import Keys
# Navegador que será usado
from selenium.webdriver import Firefox
# Configurações do drive
from selenium import webdriver
# Modulo voltado ao tempo (calendario, horas, minutos, segundos...)
import time
# Iremos usar este importe para ocultar senha (é opcional)
import getpass 
```

## Setando configurações para abrir a página web
 Como iremos aplicar este estudo usando o instagram como base, obviamente iremos usar o link do mesmo no campo url e logo após, iremos guardar as configurações para serem setadas posteriormente.
```sh
# Pegar conteúdo HTML a partir da URL
url = "https://www.instagram.com"
# todas as opções disponíveis
option = Options()
```
 Para que consigamos ver todo o processo acontecendo, é importante setarmos o valor False para o handler.
```sh
#Sete False para aparecer a págia web
option.headless = False
#Abre a aba do navegador
driver = webdriver.Firefox(options=option)
```
Como o instagram é um site responsivo, dependendo do tamanho da tela ele utiliza classes diferentes, para que o trabalho seja mais facilitado iremos setar configurações para o tamanho e posição da página Web.
```sh
#Define o tamanho da tela do navegador
driver.set_window_size(448,708)
#Define a posição da janela do navegador
driver.set_window_position(800,200)
```
Acessa o link url
```sh
#Envia o url do instagram para o navegador acessar
driver.get(url)
```

Até o momento este foi o resultado obtido:
<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82556741-baa7e900-9b40-11ea-9db0-68f9c434cd95.PNG' width='20%'>
<p/>


## Setando usuário e senha:
Agora precisamos identificar os nomes dos campos Usuário e Senha direto no navegador para que possamos posteriormente setar nossos usuários,  senhas e criar um tempo de espera para os mesmos.
Isso pode ser facilmente resolvido apertando F12 para ver o código fonte da página.

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82558320-c812a280-9b43-11ea-9c0d-aec58d9e037a.PNG' width='40%'>
<img src='https://user-images.githubusercontent.com/42920754/82558322-c8ab3900-9b43-11ea-8a61-74644cc5e0f3.PNG' width='40%'>
<p/>

Vamos primeiramente definir uma função que fará busca pelo elemento "username", para isso usamos find_element_by_name("username"), que procura tags HTML pelo nome:

```sh
def esperar_campo(firefox):
  return driver.find_element_by_name("username")
  ```
Em seguida, usaremos o WebDriverWait(driver, 5), sendo DRIVER as configurações da página web e 5 o tempo de espera até a função "espera_campo()" retornar com êxito:

```sh
carregando = WebDriverWait(driver, 5).until(esperar_campo)
```

E por fim, iremos completar os campos usuário e senha:
Para isso, e iremos usar as funções 

```sh
driver.find_element_by_name()
clear()
send_keys()
```
Para encontrar o campo, apagar qualquer dado que esteja contido e envia o usuário. O mesmo é feito para o password.
Ficando do seguinte modo:

```sh
# Insere usuário no campo
name_campo = driver.find_element_by_name("username")
name_campo.clear()
name_campo.send_keys(usuario)
```

```sh
# Insere senha no campo
senha_campo = driver.find_element_by_name("password")
senha_campo.clear()
senha_campo.send_keys(senha)
```
E por fim aperta ENTER para entrar no instagram
```sh
senha_campo.send_keys(Keys.ENTER)
```
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>



<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82489811-9e606980-9ab8-11ea-93f2-ffed391c5c37.gif' width='30%'>
<img src='https://user-images.githubusercontent.com/42920754/82492237-3e6bc200-9abc-11ea-8213-ede82c7504db.gif' width='30%'>
<p/>

<p/>
## :memo: License
This project is under the MIT license. See the [LICENSE](https://github.com/gusoliveira/webscraping-instagram/blob/master/LICENSE) for more information.

Made with by gusoliveira21 :wave: [Get in touch!](https://www.linkedin.com/in/gustavo-dami%C3%A3o-magina-de-oliveira-492b0015b/)
