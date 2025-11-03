# Projeto: Machine Learning Distribuído com Dask

Este projeto demonstra o uso do **Dask** para processamento distribuído e treinamento de modelos de Machine Learning sobre grandes volumes de dados. O exemplo utiliza **Dask-ML** para regressão logística e Random Forest, com dataset sintético gerado pelo `make_classification` e a base de dados `Mnist` disponibilizada na biblioteca `scikit-learn`.

---

## Pré-requisitos

Antes de começar, instale o Python (>= 3.11 recomendado) e `pip`.  
Os pacotes utilizados são:

```
dask
dask-ml
distributed
jupyterlab
numpy
pandas
matplotlib
requests 
aiohttp
graphviz
```

## Criando Ambiente Virtual
Para executar este projeto é necessário criar um ambiente virtual do python,
crie utilizando a seguinte linha de comando:

```
python -m venv venv
```
Em seguida, execute o seguinte comando:

### Linux    

```
source venv/bin/activate

```
### Windows

```
venv\Scripts\activate.bat

```

Em seguida, execute o seguinte comando para baixar as bibliotecas utilizadas:

```
pip install -r requirements.txt
```

## Iniciando Dask
Após esta etapa, execute o seguinte comando na máquina que será o seu scheduler do dask:

```
dask scheduler
```

Quando este comandor for executado, procure o terminal mostrará a seguinte mensagem de 
inicialização:

```
distributed.scheduler - INFO - State start
distributed.scheduler - INFO - -----------------------------------------------
distributed.scheduler - INFO -   Scheduler at:   tcp://ip_scheduler:8786
distributed.scheduler - INFO -   dashboard at:  http://ip_scheduler:8787/status
```

Após esta etapa, você poderá configurar outras máquinas como workers, utilizando o seguinte
comando:

```
dask worker tcp://ip_scheduler:8786
```

Caso deseje modificar os limites de memória e processamento das máquinas, utilize os seguintes
argumentos:

```
dask worker tcp://ip_scheduler:8786 --nthreads n°threads --memory-limit n°GB
```

Para este projeto, foram utilizados 3 computadores como workers, a partir das linhas de comando
a seguir:

```
dask worker tcp://ip_scheduler:8786 --nthreads 2 --memory-limit 6GB

dask worker tcp://ip_scheduler:8786 --nthreads 2 --memory-limit 2GB

dask worker tcp://ip_scheduler:8786 --nthreads 2 --memory-limit 4GB
```

Estes comandos limitam o uso do recurso computacional da máquina que será um worker,
caso queira utilizar todos os recursos disponíveis, utilize o seguinte comando:

```
dask worker tcp://ip_scheduler:8786
```

Para visualizar os grafos de tarefa disponíveis no notebook é necessário instalar o 
software do graphviz, através do link: https://graphviz.org/download/