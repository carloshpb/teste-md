# Requisitos prévios para ambos projetos :

* Será necessário ter o Java JDK 7 ou superior instalado e com o PATH configurado na sua máquina, conforme este [link](https://www.java.com/pt_BR/download/help/path.xml).

* Pode ser usado qualquer versão superior ao 7 para compilar, porém não pode-se adicionar funcionalidades novas que foram colocadas na versão 8 ou superior.

# 3SM Back-end

## Iniciando (baixando o projeto)

Associe sua conta com o projeto 3smbackend encontrado neste [link](https://bitbucket.org/planetarepos/3smbackend).

Tenha instalado o Git em sua máquina Linux: 

```
sudo apt install git
```

E clone o projeto:

```
git clone link-projeto
```

## Configurando o Eclipse

O projeto Back-End do **3SM** foi feito com **Maven** e funciona com **Jetty**, porém não é necessário que tenha ele instalado no sistema operacional, mas apenas uma IDE com o plugin do **Maven** e do **Jetty**.

O **Eclipse JEE** já vem com o plugin do **Maven** instalado, mas não o plugin para rodar o Jetty, que chama-se Run-Jetty_Run e encontra-se neste [link](http://marketplace.eclipse.org/content/run-jetty-run).
* A versão do Run-Jetty-Run deve ser 1.3.5 ou maior
* Caso esteja utilizando o IntelliJ, utilize o [Jetty Runner](https://plugins.jetbrains.com/plugin/7505-idea-jetty-runner)

A versão do Jetty no projeto deverá ser 6.1.26 ou maior. Para verificar qual versão está no momento, clique na aba *Run → Run Configurations…*
Na lista esquerda com os tipos de aplicações, extenda o item **Jetty Webapp** e clique no **3SM**.
Na tela, você verá a opção *Select a Jetty Version* , que deverá estar configurado para a versão 6.1.26 ou maior.

## Importando o projeto (Eclipse JEE) 

Em seguida, deve-se importar o projeto :
*File → Import… → Existing Maven Project → Browse…* e escolher o diretório do projeto

Por padrão, o projeto encontra-se no ambiente de desenvolvimento *dev*. Caso queira modificar algumas propriedades do ambiente *dev*, suas propriedades se encontram no seguinte diretório : *src/main/resources/filters/dev.properties*

Algumas das propriedades que podem ser modificadas :
*path* : Diretório onde se encontra os *reports* (*jaspers*) usados pelo projeto.
*MailContractReportTo* : Emails que receberão os reports criados pelo projeto.

## Passos iniciais após a importação

Após feito a importação, clique com o botão direito do mouse sobre o projeto na barra lateral esquerda e escolha a opção *Run As → Maven clean*

Após o clean , clique novamente com o botão direito nele : *Run As → Maven install* , para instalar as dependências do projeto.

## Rodando o projeto

Antes que vá rodar o projeto, é necessário mover os templates do jasper para gerar relatórios PDF do projeto para a sua localização definida no properties (no caso, como será ambiente de desenvolvimento, deverá utilizar o dev.properties).
Dentro do arquivo, há duas linhas que definem os diretórios dos templates que serão lidos pelo projeto :

```
#report dir
path=/opt/jaspers/3SM/melhorias_templates/
```

Todos os arquivos da pasta *3smbackend/src/main/resources/templates/* deverão ser copiados e colados no diretório definido neste path.

Após toda esta configuração, pode-se clicar com o botão direito no projeto :
*Run As → Run Jetty* para rodar o projeto.

* Caso queira fazer um simples *Build* no projeto, clique com o botão direito no projeto : *Run As → Maven Build...* e deixe definido na barra Goals o seguinte valor : *jetty:run*


# 3SM Front-End

## Iniciando (baixando o projeto)

Associe sua conta com o projeto 3smbackend encontrado neste [link](https://bitbucket.org/planetarepos/3smbackend).

Tenha instalado o Git em sua máquina Linux: 

```
sudo apt install git
```

E clone o projeto:

```
git clone link-projeto
```

## Instalando o Android-Studio

Inicialmente deve-se baixar o Android-Studio neste [link](https://developer.android.com/studio/?hl=pt-br).

Após o download, deve-se seguir o [guia de instalação](https://developer.android.com/studio/install?hl=pt-br) dele, conforme o seu sistema operacional.

## Importando o projeto e configurando o Android-Studio

* Feito a instalação, pode-se abrir (importar) o projeto no Android-Studio.
Aparecerá muitos erros após a importação, devido a vários fatores :
Será pedido para você fazer uma atualização para a última versão. Não faça quaisquer atualização automática requisitado pelas janelas de alerta do Android-Studio.

Versão do Android SDK Tools : Será reclamado da versão das ferramentas atuais no console do Android-Studio, necessitando que instale o SDK conforme os erros que aparecem no console. Instale o SDK Platform Android 4.3 (18) e todas as outras versões superiores.

* Pode ocorrer erro com a versão do properties no diretório: 

```
../3smview/_3sm/src/main/assets/compatible.versions.properties

compatible.server.version=2.3
```

Caso aconteça este erro e estiver na versão 2.3 , mude a versão 
do *compatible.server.version* para **2.2**.

* Ocorrerá um erro com a versão do Gradle. A versão do gradle pode ser encontrado no seguinte diretório :

```
../3smview/gradle/wrapper/gradle-wrapper.properties
```

Na seguinte linha :

```
distributionUrl=https\://services.gradle.org/distributions/gradle-3.3-all.zip
```

Nesta linha acima, mude o valor da versão de 3.3 para 3.5. Em seguida, clique no botão do menu *File* e clique em seguida no *Sync Project with Gradle Files* para ser feito a sincronização com a nova versão.


## Após as configurações

Já pode ser iniciado a programação do projeto! Você pode testar ele de duas formas: 

* Usando um tablet e conectando ele via USB;
* Usando o emulador do Android-Studio, que pode ser configurado conforme as intruções deste [link](https://developer.android.com/studio/run/emulator?hl=pt-br).

Caso queira fazer sincronização do Front com o Back, você rodará o Back-End no IP local de sua máquina. No Front, o arquivo que contém a constante que define o Server do Back encontra neste diretório:

```
../3smview/_3sm/src/dev/java/br/com/algarmidia/sssm/Constants.java
```

Sendo necessário mudar a seguinte linha:

```
//Desenvolvimento
public static final String SERVER = “http://3sm.algarmidia.com.br:9999/3SM”;
```

Mude o endereço dessa String para : http://seulocalhost:suaPorta/3SM
