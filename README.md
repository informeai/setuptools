# Setuptools
Setup de Envio e Publicações de Módulos Python.
## Requerimentos
twine e setuptools
```
$ pip install setuptools
$ pip install twine
```


## Criar Conta 
Criar conta no [Pypi](https://pypi.org/).

ou

Criar uma conta de Teste no [TestPypi](https://test.pypi.org/), se deseja fazer testes antes de disponibilizalo para a comunidade.

## Configuração
Criar Arquivo `.pypirc` em sua `home`, nesse arquivo irá conter informações de autenticação do `pypi` e do `testpypi`.
Apesar de não ser obrigatório a criação desse aquivo, ele facilita muito o trabalho, uma vez que você não precisará inserir email e senha toda vez que for enviar o código
```
$ home >> touch ./pypirc
```
Abra o arquivo `.pypirc` e insira as informações como no exemplo:
```
[distutils]
index-servers =
  pypi
  pypitest

[pypi]
username: seu_nomedeusuario
password: sua_senha

[pypitest]
repository: https://test.pypi.org/legacy/
username: seu_nomedeusuario
password: sua_senha
```
## Conteudo da Pasta
```
./pasta principal
├── pasta com nome do seu modulo
│   ├── main.py
│   ├── outromodulo.py
│   ├── __init__.py
│   
├── LICENSE
├── README.md
├── setup.py
```


## Arquivo Setup

```
  # -*- coding: utf-8 -*-
from setuptools import setup

setup(
    name='NOME DO MODULO',
    version='0.1.1',
    url='https://github.com/SEUPROJETO/',
    license='MIT License',
    author='AUTOR',
    author_email='EMAIL',
    keywords='python program informeai setup e outras mais...',
    description='Descrição do modulo...',
    packages=['PACOTES QUE DEVEM SER INCLUIDOS'],
    install_requires=['todos os modulos que precisam ser instalados junto com o seu'],
)
```
## Criando o Registro do Pacote
Entre na pasta pai do projeto e digite o seguinte comando:
```
$ python setup.py register --repository pypitest    # para registrar no TestPypi

OU

$ python setup.py register --repository pypi       # para registrar no Pypi
```
## Criando o /dist
O comando *sdist* vai criar a fonte de distribuição do módulo, nada mais é que um arquivo compactado do módulo.

`$ python setup.py sdist`

## Testando localmente

```
$ pip install dist/seu-modulo-0.1.tar.gz
$ python
>>> from seu-modulo import *
Olá tudo bem :)
>>>
```
## Criando o Wheels
Agora vamos criar wheels. Wheels é um pacote que já teve o seu build feito. Então você não precisa passar pelo processo de build novamente para realizar a instalação daquele pacote.
```
$ python setup.py bdist_wheel
```
A etapa anterior, gerou dentro do diretório dist/ um arquivo .whl. É esse arquivo que vamos utilizar para registrar o módulo e fazer o primeiro release. Agora vamos usar o Twine.

## Upload com o twine

```
$ twine upload dist/meu-modulo-1.0.1.whl --repository pypitest    # Envio para o TestPypi.

OU

$ twine upload dist/meu-modulo-1.0.1.whl --repository pypi    # Envio para o Pypi.
```
Tambem é possivel enviar toda a pasta `dist/`:
```
$ twine upload dist/* 
```