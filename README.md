## Instagram-WebScraping

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

- Possui versões em Inglês e Português.
- English and Portuguese versions.

## 😏 Objetivo:
<p align='Justify'>
Este tutorial visa dar uma visão simplista da biblioteca selenium, para mostrar que com poucos códigos é possível manipular uma página web e para isso, iremos usar o Anaconda como ambiente para desenvolvimento.
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

~~~python
pip install selenium
~~~

## 📚 Imports necessários:


>Espera um determinado processo.
~~~python
from selenium.webdriver.support.ui import WebDriverWait
~~~
>Importa as configurações da página web.
~~~python
from selenium.webdriver.firefox.options import Options
~~~
>Envia comandos do teclado (enter, f1, f2,...,f12).
~~~python
from selenium.webdriver.common.keys import Keys
~~~
>Importa o navegador que será usado.
~~~python
from selenium.webdriver import Firefox
~~~
>Importa as configurações do drive.
~~~python
from selenium import webdriver
~~~
>Modulo voltado ao tempo (calendario, horas, minutos, segundos...).
~~~python
import time
~~~
>Iremos usar este importe para ocultar senha (é opcional).
~~~python
import getpass 
~~~

## 🛠️ Setando configurações para abrir a página web:
<p align='Justify'>
Como iremos aplicar este estudo usando o instagram como base, obviamente iremos usar o link do mesmo no campo url e logo após, iremos guardar as configurações para serem setadas posteriormente.
<p/>

>A variável URL pega o endereço da página.
~~~python
url = "https://www.instagram.com"
~~~
>Guardamos na variável OPTION todas as opções disponíveis.
~~~python
option = Options()
~~~
<p align='Justify'>
Neste momento, é importante baixar os drives do navegador que iremos usar para que o selenium possa trabalhar e como iremos usar o Firefox para este tutorial vamos baixar o <a href='https://github.com/mozilla/geckodriver/releases'><b>Gekodriver</b><a/>, para mais informações a respeito leia a <a href='https://www.selenium.dev/documentation/en/getting_started_with_webdriver/browsers/'><b>Documentação</b><a/>.
<p/>
- Feito isso, para que consigamos visualizar todo o processo acontecendo, é importante setarmos o valor False para o handler.


>Setamos False no handless para aparecer o processo na página web.
~~~python
option.headless = False
~~~
>Abre a aba do navegador.
~~~python
driver = webdriver.Firefox(options=option)
~~~

<p align='Justify'>
Como o instagram é um site responsivo, dependendo do tamanho da tela ele utiliza classes diferentes, para que o trabalho seja mais facilitado iremos setar configurações para o tamanho e posição da página Web.
<p/>

>Definimos o tamanho da tela do navegador.
~~~python
driver.set_window_size(448,708)
~~~
>Definimos a posição da janela do navegador.
~~~python
driver.set_window_position(800,200)
~~~
>Envia o url do instagram para o driver, que enviará uma ordem para o navegador acessar o site.
~~~python
driver.get(url)
~~~

Até o momento este foi o resultado obtido: <br>
<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82556741-baa7e900-9b40-11ea-9db0-68f9c434cd95.PNG' width='20%'>
<p/>


## 🔒(***) Setando usuário e senha:

<p align="justify">
Agora precisamos identificar os nomes dos campos Usuário e Senha direto no navegador para que possamos posteriormente setar nossos usuários,  senhas e criar um tempo de espera para os mesmos.
<p/>
Isso pode ser facilmente resolvido apertando F12 para ver o código fonte da página.

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82558320-c812a280-9b43-11ea-9c0d-aec58d9e037a.PNG' width='40%'>
<img src='https://user-images.githubusercontent.com/42920754/82558322-c8ab3900-9b43-11ea-8a61-74644cc5e0f3.PNG' width='38%'>
<p/>

Vamos primeiramente definir uma função que fará uma busca pelo elemento "username", para isso usamos find_element_by_name("username"), que procura tags HTML pelo nome:


~~~python
def esperar_campo(firefox):
  return driver.find_element_by_name("username")
~~~

<p align='Justify'>
Em seguida, usaremos o WebDriverWait(driver, 5), sendo DRIVER as configurações da página web e escolhemos 5s como o tempo de espera caso a função "espera_campo()" retornar com êxito:
<p/>

~~~python
carregando = WebDriverWait(driver, 5).until(esperar_campo)
~~~

E por fim, iremos completar os campos usuário e senha:
<br>
Para isso, e iremos usar as funções 

   - driver.find_element_by_name() -> Encontrar o campo especificado com o nome.
   - clear() -> Apagar qualquer dado que esteja contido no campo.
   - send_keys() -> Envia a string para o campo encontrado.
    

Ficando do seguinte modo para o campo usuário.

>Insere dados do usuário no campo.

~~~python
name_campo = driver.find_element_by_name("username")
name_campo.clear()
name_campo.send_keys("Coloque aqui o seu usuário")
~~~

O mesmo se repete para o campo password.

>Insere senha no campo.

~~~python
senha_campo = driver.find_element_by_name("password")
senha_campo.clear()
senha_campo.send_keys("Coloque aqui a sua senha")
~~~
E por fim aperta ENTER para entrar no instagram

~~~python
senha_campo.send_keys(Keys.ENTER)
~~~

<h4> Desse modo, conseguimos obter o seguinte resultado: <h4/>

<br>
<img src='https://user-images.githubusercontent.com/42920754/82576316-16ce3580-9b60-11ea-826a-2379f22ad601.gif' width='20%'>

## ❗ Retirar notificação:

<p align='Justify'>
Com o resultado a cima conseguimos perceber o surgimento de uma janela JavaScript que irá aparecer sempre que o instagram for aberto pela primeira vez na sessão. O Selenium possue métodos para fechar janelas <a href='https://www.techbeamers.com/handle-alert-popup-selenium-python/'>(pode conferir mais aqui)<a/>, porém, vamos ver como fazer isso usando as funções que usamos até o momento.

Inicialmente, precisamos pegar as referências da janela pois vamos usar xpath, que nada mais é do que um conjunto de regras de sintaxe para definir partes de um documento XML, para seleciona-la e armazenar em variáveis. <a href='http://www.macoratti.net/vb_xpath.htm'>[2]<a/>
<p/>

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82602072-e352d180-9b86-11ea-8e2f-02762d23d2e8.PNG' width='40%'>
<img src='https://user-images.githubusercontent.com/42920754/82603081-6d4f6a00-9b88-11ea-952c-a57bcc5cd999.PNG' width='39.5%'>
<p/>

>Essas são variáveis que vou precisar, elas trazem informações do código da página! 
~~~python
dialog_box = "//div[@class='piCib']"
button_dialog_box = "//button[@class='aOOlW   HoLwm ']"
~~~

Após isso, criaremos uma função similar a função ***esperar_campo()***, e ela será chamada de ***espera_dialog()*** e irá retornar retornar uma resposta quando a dialog box carregar.

>Funcao para esperar uma resposta, caso a caixa de diálogo ainda não seja encontrada, e espera 5s após ser encontrada.

~~~python
def espera_dialog(firefox):
  return driver.find_element_by_xpath(dialog_box)
~~~

>Espera até a função ***espera_dialog()*** retornar um resultado, significando que a caixa de dialogo carregou.

~~~python
esperando_jane_dialog = WebDriverWait(driver, 10).until(espera_dialog)
~~~

>Um click é dado no botão ***"Agora não"***.

~~~python
driver.find_element_by_xpath(button_dialog_box).click()
~~~

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82611072-0cc72980-9b96-11ea-93d7-db3a2f04b923.gif' width='30%'>
<p/>

## 👀 Visualizar Story's:
Como já foi visto, o primeito passo é conseguir o endereço do botão de acesso aos storys e logo após, o botão para passar o story.

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82616860-d1802700-9ba4-11ea-9245-dc6581b51978.gif' width='30%'>
<br>
<img src='https://user-images.githubusercontent.com/42920754/82691749-c5dc4100-9c34-11ea-804f-2b8f1c41eefd.png' width='44.3%'>
<img src='https://user-images.githubusercontent.com/42920754/82691745-c4ab1400-9c34-11ea-855e-89ab41d7bdd8.png' width='40.594%'>
<p/>


<p align="justify">
Em testes, foram encontrados duas classes para os botões que precisamos, <b> class='jZyv1  H-yu6' e @class='OE3OK ' </b>, tais classes mudam de acordo com o tamanho da tela. Sendo assim, pegaremos ambas para trabalhar mesmo não tendo necessidade já que criamos uma tela 448x708 o que significa que poderemos usar somente o <b> @class='OE3OK ' </b>.
<p/>

>Guardo em variáveis o tamanho das telas disponíveis.

~~~python
window_big = "//button[@class='jZyv1  H-yu6']"
window_little = "//button[@class='OE3OK ']"
~~~

O selenium possue um método chamado Click() utilizado, como o próprio nome já diz, para dar Click em um elemento. Iremos utilizar esse método para abrir os storys.

~~~python
# Procedimento: Aperta para abrir um story
def open_story ():
    try:
     #Tela Reduzida
     driver.find_element_by_xpath(window_little).click()
    except:
     #Tela Maximizada   
     driver.find_element_by_xpath(window_big).click()
~~~
Agora, temos um botão que podemos usar para abrir os storys:

>Chamamos a função open_story()

~~~python
open_story()
~~~

<p align="justify">
Agora, por que não criamos uma função para ir passando os storys enquanto a janela de story estiver aberta ?
Pode parecer totalmente inútil, mas para algumas pessoas e trabalhos pode vir a ser útil.
Para isso, pegamos a referência a página do story para saber quando estamos ou não dentro de um story e do botão de passar visto anteriormente.
<p/>

>Diz se os story's ainda estão abertos.

~~~python
window_story ="//section[@class='_8XqED  carul']"
~~~

>É o endereço do botão para passar o story

~~~python
button_story_pass ="//button[@class='ow3u_']"
~~~

Criamos um laço de repetição que recebe diretamente o valor True, para fazer o processo indefinidamente. 
<br>
É isso que o nosso código está dizendo:
<br>
>*"Enquanto True, enquanto tiver com story aberto tente apertar o botão para passar e espere 2seg, se der erro tente esperar 1.5seg e tente passar o story novamente, se der erro atualize a página web e depois espere 8seg para abrir os storys novamente."* 

~~~python
while(True):
    try:
        while(driver.find_element_by_xpath(window_story)):
            driver.find_element_by_xpath(button_story_pass).click()
            time.sleep(2)
    except Exception as e:
        try:
            time.sleep(1.5)
            driver.find_element_by_xpath(button_story_pass).click()
        except Exception as e:
            driver.refresh()
            time.sleep(8)
            open_story()
~~~


**Este é o resultado do programa em execução:**
<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82492237-3e6bc200-9abc-11ea-8213-ede82c7504db.gif' width='30%'>
<p/>

## ❤️ Curte automaticamente publicações no instagram:
<i>Esta funcionalidade é contribuição de <a href='https://github.com/luisERH'>luisERH<a/>.</i><br>
Para esta funcionalidade nos precisamos compreender um pouco melhor o funcionamento do instagram.
<br>

- Todas as publicações ficam dentro de um flexbox.

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82713199-83c8f480-9c60-11ea-9097-c0aa20f7fc36.PNG' width='80%'>
<p/>

- E cada post fica dentro de um article.


<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82713519-9db70700-9c61-11ea-9371-a002d6be0931.png' width='80%'>
<p/>

<p align="justify"> 
Logo, se faz necessário descrever o caminho que se deve percorrer até chegar no botão que deve ser clicado. Para isso, iremos recorrer a um recurso do navegador e para usa-lo basta selecionar com o botão direito do mouse a linha a qual desejamos conseguir o endereço.
<p/>

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82713272-c68acc80-9c60-11ea-8108-29006c609dbc.png' width='80%'>
<p/>

Fazendo isso, conseguiremos o seguinte resultado:
Para saber mais sobre Seletores Css <a href='https://developer.mozilla.org/pt-BR/docs/Web/CSS/:nth-child'>clique aqui<a/>

~~~css
article._8Rm4L:nth-child(1) > div:nth-child(3) > section:nth-child(1) > span:nth-child(1) > button:nth-child(1)
~~~

<p align="justify">
Mas desse modo, conseguiremos selecionar somente o primeiro resultado a cada 8 ou 9 elementos e não é o que queremos. Para resolver este impasse, precisamos especificar mais qual elemento queremos selecionar, e neste caso são todos os elementos que não estão curtidos.
Podemos observer logo a baixo que um elemento muda dependendo do estado da publicação:
<p/>

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82716761-8f6fe780-9c6f-11ea-8f00-5379b542121a.png' width='80%'>
<p/>

Sendo assim, precisamos inserir esta condição no nosso código, ficando do seguinte modo:

~~~python
article._8Rm4L:nth-child(1n) > div:nth-child(3) > section:nth-child(1) > span:nth-child(1) > button:nth-child(1) > svg:nth-child(1)[aria-label='Curtir']
~~~

<p align="justify">
Agora, vamos criar uma função chamada <b> curte_publicacoes() </b> com um <b> Try Catch </b> para curtir os elementos encontrados e em caso de alguma excessão, usamos o atributo <b> PASS </b> que significa passar, ou seja, deixa passar a ocorrência.
<p/>

~~~python
def curte_publicacoes():
    try:
        driver.find_element_by_css_selector("article._8Rm4L:nth-child(1n) > div:nth-child(3) > section:nth-child(1) > span:nth-child(1) > button:nth-child(1) > svg:nth-child(1)[aria-label='Curtir']").click()
    except Exception as e:
        pass
~~~

<p align="justify">
E por fim, criamos um While com o valor True, para roda-lo indefinidamente, dentro, iremos criar um acumulador chamado de aux (auxiliar), que crescera em 100 a cada volta completa. Usaremos a função de manipulação de Script do selenium (driver.execute_script()) para manipular o scroll roll da página, e para isso usaremos uma função em Script que pode ser chamada assim -> window.scrollTo(Horizontal,Vertical), e logo em seguida, chamaremos a função criada anteriormente, deixando o código do seguinte modo:
<p/>

~~~python
#Desde página
aux = 1
while(True):
    aux += 100
    driver.execute_script(f'window.scrollTo(0,{aux})')
    curte_publicacoes()            
~~~

- O resultado final:

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82489811-9e606980-9ab8-11ea-93f2-ffed391c5c37.gif' width='30%'>
<p/>

## 🎯 Próximas atualizações:
- "Quando chegar no limite da página, atualizar página".
- OBS: O código é bem simples e devido a isso acaba tendo alguns bugs.

## 🤝 Contribua com este pequeno projeto 💙

- Faça um fork desse repositório;
- Cria uma branch com a sua feature: `git checkout -b minha-feature`;
- Faça commit das suas alterações: `git commit -m 'feat: Minha nova feature'`;
- Faça push para a sua branch: `git push origin minha-feature`.

Depois que o merge da sua pull request for feito, você pode deletar a sua branch.


## :memo: License

This project is under the MIT license. See the [LICENSE](https://github.com/gusoliveira/webscraping-instagram/blob/master/LICENSE) for more information.

Made with by gusoliveira21 :wave: [Get in touch!](https://www.linkedin.com/in/gustavo-dami%C3%A3o-magina-de-oliveira-492b0015b/)



## ☕ Donation

Se este projeto lhe ajudou de alguma forma não esqueça de contribuir para o café desse dev! :)

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=P87GHQLSDSJU2&source=url)


### Inglês:
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

## 😏 objective:
<p align='Justify'>
This tutorial aims to give a simplistic view of the selenium library, to show that with few codes it is possible to manipulate a web page and for that, we will use Anaconda as a development environment.
<p/>

## What is selenium ❓
<p align='Justify'>
Selenium is a lib that allows you to define tests and automatically detect the results of those tests in a preferred browser. A set of Selenium functions makes it possible to create step-by-step interactions with a web page, simulating a normal user of the system.
<a href='https://www.browserstack.com/guide/python-selenium-to-run-web-automation-test'>[1]<a/>
<p/>
 
## 💿 How to install:
<p align='Justify'>
To install Selenium just run in this way the library will be downloaded to your Anaconda environment: <br>
<p/>

~~~python
pip install selenium
~~~

## 📚 Necessary Imports:


>Expects a certain process.
~~~python
from selenium.webdriver.support.ui import WebDriverWait
~~~
>Import web page settings.
~~~python
from selenium.webdriver.firefox.options import Options
~~~
>Send keyboard commands (enter, f1, f2,...,f12).
~~~python
from selenium.webdriver.common.keys import Keys
~~~
>Import the browser to be used.
~~~python
from selenium.webdriver import Firefox
~~~
>Import drive settings.
~~~python
from selenium import webdriver
~~~
>Time-oriented module (calendar, hours, minutes, seconds ...).
~~~python
import time
~~~
>We will use this item to hide password (optional).
~~~python
import getpass 
~~~

## 🛠️ Setting settings to open the web page:
<p align='Justify'>
As we will apply this study using instagram as a base, obviously we will use its link in the url field and soon after, we will save the settings to be set later.
<p/>

>The URL variable takes the page address.
~~~python
url = "https://www.instagram.com"
~~~
>We keep all available options in the OPTION variable.
~~~python
option = Options()
~~~
<p align='Justify'>
At this point, it is important to download the browser drivers that we will be using so that selenium can work and as we will be using Firefox for this tutorial we will download the <a href='https://github.com/mozilla/geckodriver/releases'><b>Gekodriver</b><a/>, for more information on this read the <a href='https://www.selenium.dev/documentation/en/getting_started_with_webdriver/browsers/'><b>documentation</b><a/>.
<p/>
- That done, so that we can visualize the whole process happening, it is important to set the value False to handler.


>We set False on handless to show the process on the web page.
~~~python
option.headless = False
~~~
>Opens the browser tab.
~~~python
driver = webdriver.Firefox(options=option)
~~~

<p align='Justify'>
As instagram is a responsive site, depending on the size of the screen it uses different classes, so that work is easier we will set up settings for the size and position of the web page.
<p/>

>We set the browser screen size.
~~~python
driver.set_window_size(448,708)
~~~
>We define the position of the browser window.
~~~python
driver.set_window_position(800,200)
~~~
>Send the instagram url to the driver, who will send an order to the browser to access the site.
~~~python
driver.get(url)
~~~

So far this has been the result obtained: <br>
<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82556741-baa7e900-9b40-11ea-9db0-68f9c434cd95.PNG' width='20%'>
<p/>


## 🔒(***) Setting username and password:

<p align="justify">
Now we need to identify the User and Password field names directly in the browser so that we can later set our users, passwords and create a timeout for them.
<p/>
This can be easily resolved by pressing F12 to see the source code of the page.

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82558320-c812a280-9b43-11ea-9c0d-aec58d9e037a.PNG' width='40%'>
<img src='https://user-images.githubusercontent.com/42920754/82558322-c8ab3900-9b43-11ea-8a61-74644cc5e0f3.PNG' width='38%'>
<p/>

Let's first define a function that will do a search for the element "username", for that we use find_element_by_name ("username"), which looks for HTML tags by name:


~~~python
def esperar_campo(firefox):
  return driver.find_element_by_name("username")
~~~

<p align='Justify'>
Then, we will use WebDriverWait (driver, 5), DRIVER the settings of the web page and choose 5s as the waiting time if the function "hold_field ()" returns successfully:
<p/>

~~~python
carregando = WebDriverWait(driver, 5).until(esperar_campo)
~~~

And finally, we will complete the username and password fields:
<br>
For that, and we will use the functions

   - driver.find_element_by_name() -> Find the specified field with the name.
   - clear() -> Delete any data that is contained in the field.
   - send_keys() -> Send the string to the found field.
    

Staying as follows for the user field.

>Insert user data in the field.

~~~python
name_campo = driver.find_element_by_name("username")
name_campo.clear()
name_campo.send_keys("Coloque aqui o seu usuário")
~~~

The same is repeated for the password field.

>Enter password in the field.

~~~python
senha_campo = driver.find_element_by_name("password")
senha_campo.clear()
senha_campo.send_keys("Coloque aqui a sua senha")
~~~
And finally press ENTER to enter instagram

~~~python
senha_campo.send_keys(Keys.ENTER)
~~~

<h4> In this way, we were able to obtain the following result: <h4/>

<br>
<img src='https://user-images.githubusercontent.com/42920754/82576316-16ce3580-9b60-11ea-826a-2379f22ad601.gif' width='20%'>

## ❗ Retirar notificação:

<p align='Justify'>
With the result above we can see the appearance of a JavaScript window that will appear whenever instagram is opened for the first time in the session. Selenium has methods for closing windows <a href='https://www.techbeamers.com/handle-alert-popup-selenium-python/'> (you can check more here) <a/>, however, let's see how do this using the functions we've used so far.

Initially, we need to get the window references because we are going to use xpath, which is nothing more than a set of syntax rules to define parts of an XML document, to select it and store it in variables. <a href='http://www.macoratti.net/vb_xpath.htm'> [2] <a/>
<p/>

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82602072-e352d180-9b86-11ea-8e2f-02762d23d2e8.PNG' width='40%'>
<img src='https://user-images.githubusercontent.com/42920754/82603081-6d4f6a00-9b88-11ea-952c-a57bcc5cd999.PNG' width='39.5%'>
<p/>

>These are variables that I will need, they bring information from the page code!
~~~python
dialog_box = "//div[@class='piCib']"
button_dialog_box = "//button[@class='aOOlW   HoLwm ']"
~~~

After that, we will create a function similar to the *** esper_campo () *** function, and it will be called *** awa_dialog () *** and will return a response when the dialog box loads.

>Function to wait for a response, if the dialog box is still not found, and wait 5s after being found.

~~~python
def espera_dialog(firefox):
  return driver.find_element_by_xpath(dialog_box)
~~~

>Wait until the ***hold_dialog()*** function returns a result, meaning that the dialog box has loaded.

~~~python
esperando_jane_dialog = WebDriverWait(driver, 10).until(espera_dialog)
~~~

>A click is given on the button ***"Not now"***.

~~~python
driver.find_element_by_xpath(button_dialog_box).click()
~~~

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82611072-0cc72980-9b96-11ea-93d7-db3a2f04b923.gif' width='30%'>
<p/>

## 👀 View Story's:
As already seen, the first step is to get the address of the button to access the storys and soon after, the button to pass the story.

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82616860-d1802700-9ba4-11ea-9245-dc6581b51978.gif' width='30%'>
<br>
<img src='https://user-images.githubusercontent.com/42920754/82691749-c5dc4100-9c34-11ea-804f-2b8f1c41eefd.png' width='44.3%'>
<img src='https://user-images.githubusercontent.com/42920754/82691745-c4ab1400-9c34-11ea-855e-89ab41d7bdd8.png' width='40.594%'>
<p/>


<p align="justify">
In tests, two classes were found for the buttons we need, <b> class='jZyv1  H-yu6' and @class='OE3OK ' </b>, such classes change according to the size of the screen. Therefore, we will take both to work even if we don’t need it since we created a screen 448x708 which means that we can only use the <b> @class='OE3OK ' </b>.
<p/>

>I keep the size of the available screens in variables.

~~~python
window_big = "//button[@class='jZyv1  H-yu6']"
window_little = "//button[@class='OE3OK ']"
~~~

Selenium has a method called Click () used, as the name implies, to click on an element. We will use this method to open the storys.

~~~python
# Procedure: Press to open a story
def open_story ():
    try:
     #Reduced Screen
     driver.find_element_by_xpath(window_little).click()
    except:
     #Maximized Screen  
     driver.find_element_by_xpath(window_big).click()
~~~
Now, we have a button that we can use to open the storys:

>We call the open_story function()

~~~python
open_story()
~~~

<p align="justify">
Now, why don't we create a function to go through the storys while the story window is open?
It may seem totally useless, but for some people and jobs it can prove to be useful.
For that, we take the reference to the story page to know when or not we are inside a story and the pass button seen previously.<p/>

>Tell if the stories are still open.

~~~python
window_story ="//section[@class='_8XqED  carul']"
~~~

>It is the address of the button to pass the story

~~~python
button_story_pass ="//button[@class='ow3u_']"
~~~

We created a loop that directly receives the value True, to do the process indefinitely.
<br>
That's what our code is saying:
<br>
>*"While Truth, while you have an open story try to press the button to pass and wait 2 seconds, if it fails try to wait 1.5 seconds and try to pass the story again, if it fails, refresh the web page and then wait 8 seconds to open the stories again."* 

~~~python
while(True):
    try:
        while(driver.find_element_by_xpath(window_story)):
            driver.find_element_by_xpath(button_story_pass).click()
            time.sleep(2)
    except Exception as e:
        try:
            time.sleep(1.5)
            driver.find_element_by_xpath(button_story_pass).click()
        except Exception as e:
            driver.refresh()
            time.sleep(8)
            open_story()
~~~


**This is the result of the running program:**
<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82492237-3e6bc200-9abc-11ea-8213-ede82c7504db.gif' width='30%'>
<p/>

## ❤️ Automatically like posts on instagram:
<i>This feature is contributed by <a href='https://github.com/luisERH'>luisERH<a/>.</i><br>
For this functionality we need to understand a little better how instagram works.
<br>

- All publications are inside a flexbox.

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82713199-83c8f480-9c60-11ea-9097-c0aa20f7fc36.PNG' width='80%'>
<p/>

- And each post is inside an article.


<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82713519-9db70700-9c61-11ea-9371-a002d6be0931.png' width='80%'>
<p/>

<p align="justify"> 
Therefore, it is necessary to describe the path to be followed until reaching the button to be clicked. For this, we will use a browser feature and to use it just select with the right mouse button the line to which we want to get the address.
<p/>

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82713272-c68acc80-9c60-11ea-8108-29006c609dbc.png' width='80%'>
<p/>

By doing this, we achieve the following result:
To learn more about Selectors Css <a href='https://developer.mozilla.org/pt-BR/docs/Web/CSS/:nth-child'>clique aqui<a/>

~~~css
article._8Rm4L:nth-child(1) > div:nth-child(3) > section:nth-child(1) > span:nth-child(1) > button:nth-child(1)
~~~

<p align="justify">
But in this way, we will be able to select only the first result every 8 or 9 elements and it is not what we want. To resolve this impasse, we need to specify more which element we want to select, and in this case it is all the elements that are not tanned.
We can see below that an element changes depending on the state of the publication:
<p/>

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82716761-8f6fe780-9c6f-11ea-8f00-5379b542121a.png' width='80%'>
<p/>

Therefore, we need to insert this condition in our code, being as follows:

~~~python
article._8Rm4L:nth-child(1n) > div:nth-child(3) > section:nth-child(1) > span:nth-child(1) > button:nth-child(1) > svg:nth-child(1)[aria-label='Curtir']
~~~

<p align="justify">
Now, let's create a function called <b> Likes_publicacoes() </b> with a <b> Try Catch </b> to like the found elements and in case of any exception, we use the <b> PASS </b> attribute which means to pass, that is, to let the occurrence pass.
<p/>

~~~python
def curte_publicacoes():
    try:
        driver.find_element_by_css_selector("article._8Rm4L:nth-child(1n) > div:nth-child(3) > section:nth-child(1) > span:nth-child(1) > button:nth-child(1) > svg:nth-child(1)[aria-label='Curtir']").click()
    except Exception as e:
        pass
~~~

<p align="justify">
And finally, we created a While with the value True, to run it indefinitely, inside, we will create an accumulator called aux (auxiliary), which will grow by 100 with each complete lap. We will use selenium's Script manipulation function (driver.execute_script()) to manipulate the page's scroll roll, and for that we will use a script function that can be called like this -> window.scrollTo (Horizontal, Vertical), and then then we will call the function created earlier, leaving the code as follows:
<p/>

~~~python
#From page
aux = 1
while(True):
    aux += 100
    driver.execute_script(f'window.scrollTo(0,{aux})')
    curte_publicacoes()            
~~~

- The final result:

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82489811-9e606980-9ab8-11ea-93f2-ffed391c5c37.gif' width='30%'>
<p/>

## 🎯 Upcoming updates:
- "When you reach the page border, refresh page".
- OBS: The code is very simple and due to this it ends up having some bugs.

## 🤝 Contribute to this small project 💙

- Fork this repository;
- Create a branch with your feature: `git checkout -b my-feature`;
- Commit your changes: `git commit -m 'feat: My new feature'`;
- Push to your branch: `git push origin my-feature`.

After the merge of your pull request is done, you can delete your branch.


## :memo: License

This project is under the MIT license. See the [LICENSE](https://github.com/gusoliveira/webscraping-instagram/blob/master/LICENSE) for more information.

Made with by gusoliveira21 :wave: [Get in touch!](https://www.linkedin.com/in/gustavo-dami%C3%A3o-magina-de-oliveira-492b0015b/)



## ☕ Donation

If this project helped you in any way don't forget to contribute to that dev's coffee! :)

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=P87GHQLSDSJU2&source=url)

