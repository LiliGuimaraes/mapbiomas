<p align="center">
<img src ="https://github.com/saraivaufc/mapbiomas/blob/master/docs/images/logo.svg" />
</p>

<p align="justify">
O Projeto MapBiomas é uma iniciativa que envolve uma rede colaborativa de especialistas em diversos temas, atuantes nos biomas brasileiros, com o objetivo principal de elaborar mapas anuais de cobertura vegetal e uso do solo para todo o Brasil. O propósito original de tais mapas é preencher lacunas de informação sobre a dinâmica da cobertura do solo e reduzir incertezas das estimativas de emissões de gases de efeito estufa associadas a esse processo, mas as aplicações certamente serão muito mais amplas.
</p>
<p align="justify">
A iniciativa MapBiomas conta com participação de instituições públicas, privadas e organizações não governamentais (ONGs), com apoio de recursos internacionais para viabilizar o desenvolvimento das atividades. A proposta está baseada na utilização de processamento em nuvem, a partir da plataforma Google Earth Engine, para selecionar, processar e efetuar a classificação digital de imagens de satélite. 
<p>

<div>
  <img src ="https://github.com/saraivaufc/mapbiomas/blob/master/docs/images/brasil.jpg" />
</div>

<div align="justify">
  <img  src="https://github.com/saraivaufc/mapbiomas/blob/master/docs/images/amazonia.jpg" width="33%" />
  <img src ="https://github.com/saraivaufc/mapbiomas/blob/master/docs/images/cerrado-a.jpg" width="33%" />
  <img src ="https://github.com/saraivaufc/mapbiomas/blob/master/docs/images/mata-atlantica.jpg" width="33%" />
</div>
<div>
  <img src="https://github.com/saraivaufc/mapbiomas/blob/master/docs/images/pampa.jpg" width="33%" />
  <img src ="https://github.com/saraivaufc/mapbiomas/blob/master/docs/images/pantanal.jpg" width="33%" />
  <img src ="https://github.com/saraivaufc/mapbiomas/blob/master/docs/images/caatinga.jpg" width="33%" />
<//div>

# Instructions

Install Google Cloud SDK

https://cloud.google.com/sdk/docs/#deb

```
$ export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)"
$ echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
$ curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
$ sudo apt-get update && sudo apt-get install google-cloud-sdk
$ gcloud init 
$ gcloud auth application-default login
```

Install python libraries

https://cloud.google.com/storage/docs/reference/libraries#client-libraries-install-python

```
$ pip install --upgrade google-cloud-storage
$ earthengine authenticate
```

Install postgres 9.5:
```
$ sudo apt-get install postgresql-9.5 postgresql-server-dev-9.5
$ sudo -u postgres psql
$ \password postgres
```

Create a database
```
$ psql -U postgres -W -h localhost
$ create database mapbiomas;
```

Create a virtual environment
```
$ virtualenv env
$ source env/bin/activate
```

Install requirements
```
$ pip install -r rsgee/requirements.txt
```

Initialize database:
```
>> from rsgee.db import DatabaseManager
>> db = DatabaseManager()
>> db.migrate()
```

To use client API, install ImageTk

```
sudo apt-get install python-imaging-tk
```
and alter in ee/mapclient.py from

```
import ImageTk
import Image
```

to

```
from PIL import ImageTk
from PIL import Image
```

Create your settings or use an existing, change "mapbiomas/settings/__init__.py" to choose the settings.
