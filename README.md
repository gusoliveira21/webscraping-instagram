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

## 🛠️ Setando configurações para abrir a página web:
<p align='Justify'>
Como iremos aplicar este estudo usando o instagram como base, obviamente iremos usar o link do mesmo no campo url e logo após, iremos guardar as configurações para serem setadas posteriormente.
<p/>

```sh
# Pegar conteúdo HTML a partir da URL
url = "https://www.instagram.com"
# pega todas as opções disponíveis
option = Options()
```

Para que consigamos ver todo o processo acontecendo, é importante setarmos o valor False para o handler.

```sh
#Sete False no handless para aparecer o processo na págia web
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

Acessa o link url

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

Vamos primeiramente definir uma função que fará uma busca pelo elemento "username", para isso usamos find_element_by_name("username"), que procura tags HTML pelo nome:


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

<p align='Justify'>
Com o resultado a cima conseguimos perceber o surgimento de uma janela JavaScript que irá aparecer sempre que o instagram for aberto pela primeira vez na sessão. O Selenium possue métodos para fechar janelas <a href='https://www.techbeamers.com/handle-alert-popup-selenium-python/'>(pode conferir mais aqui)<a/>, porém, vamos ver como fazer isso usando as funções que usamos até o momento.

Inicialmente, precisamos pegar as referências da janela pois vamos usar xpath, que nada mais é do que um conjunto de regras de sintaxe para definir partes de um documento XML, para seleciona-la e armazenar em variáveis. <a href='http://www.macoratti.net/vb_xpath.htm'>[2]<a/>
<p/>

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82602072-e352d180-9b86-11ea-8e2f-02762d23d2e8.PNG' width='40%'>
<img src='https://user-images.githubusercontent.com/42920754/82603081-6d4f6a00-9b88-11ea-952c-a57bcc5cd999.PNG' width='39.5%'>
<p/>

```sh
#Variáveis que vou precisar, elas trazem informações do código da página! 
dialog_box = "//div[@class='piCib']"
button_dialog_box = "//button[@class='aOOlW   HoLwm ']"
```

Após, criaremos uma função similar a função ***esperar_campo()***, e ela será chamada de ***espera_dialog()*** e irá retornar retornar uma resposta quando a dialog box carregar.

```sh
# Funcao para esperar caso a caixa de diálogo ainda não seja encontrada, e espera 5s se for.
def espera_dialog(firefox):
  return driver.find_element_by_xpath(dialog_box)
```

Espera até a função ***espera_dialog()*** retornar um resultado, significando que a caixa de dialogo carregou.

```sh
esperando_jane_dialog = WebDriverWait(driver, 10).until(espera_dialog)
```

Damos um click no botão ***"Agora não"***.

```sh
driver.find_element_by_xpath(button_dialog_box).click()
```

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

```sh
#Variáveis do tamanho da tela
window_big = "//button[@class='jZyv1  H-yu6']"
window_little = "//button[@class='OE3OK ']"
```

O selenium possue um método chamado Click() utilizado, como o próprio nome já diz, para dar Click em um elemento. Iremos utilizar esse método para abrir os storys.

```sh
# Procedimento: Aperta para abrir um story
def open_story ():
    try:
     #Tela Reduzida
     driver.find_element_by_xpath(window_little).click()
    except:
     #Tela Maximizada   
     driver.find_element_by_xpath(window_big).click()
```
Agora, temos um botão que podemos usar para abrir os storys:

```sh
#Abre o story
open_story()
```
<p align="justify">
Agora, por que não criamos uma função para ir passando os storys enquanto a janela de story estiver aberta ?
Pode parecer totalmente inútil, mas para algumas pessoas e trabalhos pode vir a ser útil.
Para isso, pegamos a referência a página do story para saber quando estamos ou não dentro de um story e do botão de passar visto anteriormente.
<p/>

```sh
#window_story: Diz se os story's ainda estão abertos
window_story ="//section[@class='_8XqED  carul']"
#button_story_pass: É o endereço do botão para passar o story
button_story_pass ="//button[@class='ow3u_']"
```

Criamos um laço de repetição que recebe diretamente o valor True, para fazer o processo indefinidamente. 
<br>
É isso que o nosso código está dizendo:
<br>
*"Enquanto tiver story, tente apertar o botão para passar e espere 0.2seg, se der erro significa que acabou os story's, sendo assim, espere 1seg e abra novamente o story."* 


```sh
#Abre os story's e vai passando
while(True):
    # Enquanto ainda tiver story, tente apertar no botão, se der erro, espere
    try:
        while(driver.find_element_by_xpath(window_story)):
            driver.find_element_by_xpath(button_story_pass).click()
            time.sleep(0.2)
    except Exception as e:
        time.sleep(1)
        #espera_story_func(firefox)
        #esperando_story = WebDriverWait(driver, 5).until(espera_story_func)
        open_story()
```

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
Para saber mais sobre Seletores Css <a href='https://developer.mozilla.org/pt-BR/docs/Web/CSS/:nth-child'>clique aqui</>

```sh
article._8Rm4L:nth-child(1) > div:nth-child(3) > section:nth-child(1) > span:nth-child(1) > button:nth-child(1)
```
<p align="justify">
Mas desse modo, conseguiremos selecionar somente o primeiro resultado a cada 8 ou 9 elementos e não é o que queremos. Para resolver este impasse, precisamos especificar mais qual elemento queremos selecionar, e neste caso são todos os elementos que não estão curtidos.
Podemos observer logo a baixo que um elemento muda dependendo do estado da publicação:
<p/>

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82716761-8f6fe780-9c6f-11ea-8f00-5379b542121a.png' width='80%'>
<p/>

Sendo assim, precisamos inserir esta condição no nosso código, ficando do seguinte modo:

```sh
article._8Rm4L:nth-child(1n) > div:nth-child(3) > section:nth-child(1) > span:nth-child(1) > button:nth-child(1) > svg:nth-child(1)[aria-label='Curtir']
```

<p align="justify">
Agora, vamos criar uma função chamada <b> curte_publicacoes() <b/> com um <b> Try Catch <b/> para curtir os elementos encontrados e em caso de alguma excessão, usamos o atributo <b> PASS <b/> que significa passar, ou seja, deixa passar a ocorrência.
<p/>

```sh
def curte_publicacoes():
    try:
        driver.find_element_by_css_selector("article._8Rm4L:nth-child(1n) > div:nth-child(3) > section:nth-child(1) > span:nth-child(1) > button:nth-child(1) > svg:nth-child(1)[aria-label='Curtir']").click()
    except Exception as e:
        pass
```
<p align="justify">
E por fim, criamos um While com o valor True, para roda-lo indefinidamente, dentro, iremos criar um acumulador chamado de aux (auxiliar), que crescera em 100 a cada volta completa. Usaremos a função de manipulação de Script do selenium (driver.execute_script()) para manipular o scroll roll da página, e para isso usaremos uma função em Script que pode ser chamada assim -> window.scrollTo(Horizontal,Vertical), e logo em seguida, chamaremos a função criada anteriormente, deixando o código do seguinte modo:
<p/>

```sh    
#Desde página
aux = 1
while(True):
    aux += 100
    driver.execute_script(f'window.scrollTo(0,{aux})')
    curte_publicacoes()            
```

- O resultado final:

<p align="center">
<img src='https://user-images.githubusercontent.com/42920754/82489811-9e606980-9ab8-11ea-93f2-ffed391c5c37.gif' width='30%'>
<p/>

## :memo: License

This project is under the MIT license. See the [LICENSE](https://github.com/gusoliveira/webscraping-instagram/blob/master/LICENSE) for more information.

Made with by gusoliveira21 :wave: [Get in touch!](https://www.linkedin.com/in/gustavo-dami%C3%A3o-magina-de-oliveira-492b0015b/)



## ☕ Donation

Se este projeto lhe ajudou de alguma forma não esqueça de contribuir para o café desse dev! :)

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=P87GHQLSDSJU2&source=url)
