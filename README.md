## instagram-webscraping

<p align="center">
<a href='https://www.selenium.dev/'>
<img width="20%" alt="selenium_logo_large" src="https://user-images.githubusercontent.com/42920754/82577481-6bbe7b80-9b61-11ea-997e-840983ab05fd.png">
<a/>
 <a href='https://www.anaconda.com/'>
<img width="20%" alt="selenium_logo_large" src="https://user-images.githubusercontent.com/42920754/82577832-ee473b00-9b61-11ea-85c5-58011d17b0e8.PNG">
<a/>
<p/>
 
<p align="center">
<a href="https://github.com/SeleniumHQ/selenium">
<img src="https://img.shields.io/badge/built%20with-Selenium-yellow.svg" />
</a>
<a href="https://www.python.org/">
<img src="https://img.shields.io/badge/built%20with-Python3-red.svg" />
</a>
<p/>

## 😏 Objetivo:
<p align='Justify'>
Este tutorial visa dar uma visão simplista da biblioteca selenium, para agilizar o aprendizado de novos usuários nos estudos da mesma. Para isso, iremos usar o Anaconda como ambiente para desenvolvimento.
<p/>

## O que é o selenium ❓
<p align='Justify'>
O Selenium é uma lib que permite definir testes e detectar automaticamente os resultados desses testes em um navegador preferido. Um conjunto de funções do Selenium possibilita criar interações passo a passo com uma página da web, simulando um usuário normal do sistema.
<a href='https://www.browserstack.com/guide/python-selenium-to-run-web-automation-test'>[1]<a/>
<p/>
 
## 💿 Como instalar:
<p align='Justify'>
Para instalar o Selenium basta executar desse modo a biblioteca será baixada para o seu ambiente Anaconda: <br>
<p/>

```sh
pip install selenium
```

## 📚 Imports necessários:
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

## 🛠️ Setando configurações para abrir a página web
<p align='Justify'>
Como iremos aplicar este estudo usando o instagram como base, obviamente iremos usar o link do mesmo no campo url e logo após, iremos guardar as configurações para serem setadas posteriormente.
<p/>

```sh
# Pegar conteúdo HTML a partir da URL
url = "https://www.instagram.com"
# todas as opções disponíveis
option = Options()
```

<p align='Justify'>
Para que consigamos ver todo o processo acontecendo, é importante setarmos o valor False para o handler.
<p/>

```sh
#Sete False para aparecer a págia web
option.headless = False
#Abre a aba do navegador
driver = webdriver.Firefox(options=option)
```

<p align='Justify'>
Como o instagram é um site responsivo, dependendo do tamanho da tela ele utiliza classes diferentes, para que o trabalho seja mais facilitado iremos setar configurações para o tamanho e posição da página Web.
<p/>

```sh
#Define o tamanho da tela do navegador
driver.set_window_size(448,708)
#Define a posição da janela do navegador
driver.set_window_position(800,200)
```

<p align='Justify'>
Acessa o link url
<p/>

```sh
#Envia o url do instagram para o navegador acessar
driver.get(url)
```

Até o momento este foi o resultado obtido: <br>
<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82556741-baa7e900-9b40-11ea-9db0-68f9c434cd95.PNG' width='20%'>
<p/>


## 🔒(***) Setando usuário e senha:

Agora precisamos identificar os nomes dos campos Usuário e Senha direto no navegador para que possamos posteriormente setar nossos usuários,  senhas e criar um tempo de espera para os mesmos.
Isso pode ser facilmente resolvido apertando F12 para ver o código fonte da página.

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82558320-c812a280-9b43-11ea-9c0d-aec58d9e037a.PNG' width='40%'>
<img src='https://user-images.githubusercontent.com/42920754/82558322-c8ab3900-9b43-11ea-8a61-74644cc5e0f3.PNG' width='38%'>
<p/>

<p align='Justify'>
Vamos primeiramente definir uma função que fará busca pelo elemento "username", para isso usamos find_element_by_name("username"), que procura tags HTML pelo nome:
<p/>

```sh
def esperar_campo(firefox):
  return driver.find_element_by_name("username")
  ```
  
<p align='Justify'>
Em seguida, usaremos o WebDriverWait(driver, 5), sendo DRIVER as configurações da página web e escolhemos 5s como o tempo de espera caso a função "espera_campo()" retornar com êxito:
<p/>

```sh
carregando = WebDriverWait(driver, 5).until(esperar_campo)
```

E por fim, iremos completar os campos usuário e senha:
<br>
Para isso, e iremos usar as funções 

   <ul> 
        <li>driver.find_element_by_name() -> Encontrar o campo especificado com o nome. </li> 
        <li>clear() -> Apagar qualquer dado que esteja contido no campo.</li> 
        <li>send_keys() -> Envia a string para o campo encontrado.</li> 
    </ul>
    

Ficando do seguinte modo para o campo usuário.
 
```sh
# Insere usuário no campo
name_campo = driver.find_element_by_name("username")
name_campo.clear()
name_campo.send_keys("Coloque aqui o seu usuário")
```

O mesmo se repete para o campo password.

```sh
# Insere senha no campo
senha_campo = driver.find_element_by_name("password")
senha_campo.clear()
senha_campo.send_keys("Coloque aqui a sua senha")
```
E por fim aperta ENTER para entrar no instagram

```sh
senha_campo.send_keys(Keys.ENTER)
```

<h4> Desse modo, conseguimos obter o seguinte resultado: <h4/>

<br>
<img src='https://user-images.githubusercontent.com/42920754/82576316-16ce3580-9b60-11ea-826a-2379f22ad601.gif' width='20%'>

## ❗ Retirar notificação:

Com o resultado a cima conseguimos perceber o surgimento de uma janela JavaScript que irá aparecer sempre que o instagram for aberto pela primeira vez na sessão. O Selenium possue métodos para fechar janelas <a href='https://www.techbeamers.com/handle-alert-popup-selenium-python/'>(pode conferir mais aqui)<a/>, porém, vamos ver como fazer isso usando as funções que usamos até o momento.

Inicialmente, precisamos pegar as referências da janela pois vamos usar xpath para seleciona-la, que nada mais é do que um conjunto de regras de sintaxe para definir partes de um documento XML. <a href='http://www.macoratti.net/vb_xpath.htm'>[2]<a/>

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82602072-e352d180-9b86-11ea-8e2f-02762d23d2e8.PNG' width='40%'>
<img src='https://user-images.githubusercontent.com/42920754/82603081-6d4f6a00-9b88-11ea-952c-a57bcc5cd999.PNG' width='39.5%'>
<p/>

```sh
#Variáveis que vou precisar, elas trazem informações do código da página! 
dialog_box = "//div[@class='piCib']"
button_dialog_box = "//button[@class='aOOlW   HoLwm ']"

# Funcao para esperar caso a caixa de diálogo ainda não seja encontrada, e espera 5s se for.
def espera_dialog(firefox):
  return driver.find_element_by_xpath(dialog_box)

# Espera janela de dialogo inicial
esperando_jane_dialog = WebDriverWait(driver, 10).until(espera_dialog)

# Aperta para fechar caixa de dialogo
driver.find_element_by_xpath(button_dialog_box).click()
```


















-------------------------------------------------------------------------------------------------------------------
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82489811-9e606980-9ab8-11ea-93f2-ffed391c5c37.gif' width='40%'>
<img src='https://user-images.githubusercontent.com/42920754/82492237-3e6bc200-9abc-11ea-8213-ede82c7504db.gif' width='40%'>
<p/>

## :memo: License

This project is under the MIT license. See the [LICENSE](https://github.com/gusoliveira/webscraping-instagram/blob/master/LICENSE) for more information.

Made with by gusoliveira21 :wave: [Get in touch!](https://www.linkedin.com/in/gustavo-dami%C3%A3o-magina-de-oliveira-492b0015b/)
