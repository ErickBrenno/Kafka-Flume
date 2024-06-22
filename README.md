# Kafka e Apache Flume

## Introdução
Nessa documentação, abordaremos os conceitos e práticas essenciais para a utilização do Apache Flume e Apache Kafka, duas ferramentas amplamente utilizadas para coleta, transporte e processamento de dados em tempo real.

## Configuração do Ambiente com VirtualBox
Nesta seção, vamos orientá-lo sobre como importar um ambiente pré-configurado utilizando o VirtualBox. Isso incluirá a importação de uma máquina virtual que já possui Apache Flume e Apache Kafka instalados e configurados.

### *Passo 1: Instalação do VirtualBox*
- Baixe o VirtualBox a partir do site oficial.
- Siga as instruções de instalação fornecidas pelo instalador.

### *Passo 2: Download do Arquivo da Máquina Virtual*
- Obtenha o arquivo da máquina virtual pré-configurada no Canvas (geralmente um arquivo com extensão .ova ou .ovf).
- Dentro do Virtual Box, clique em "Importar".

![image](https://github.com/ErickBrenno/Kafka-Flume/assets/83048005/5fd39c1b-9663-4e54-938f-cf8c956527ab)
- Na tela seguinte, selecione a opção "Escolha um arquivo para importar o appliance virtual".
- Após isso, selecione o arquivo para a exportação no Virtual Box.

![image](https://github.com/ErickBrenno/Kafka-Flume/assets/83048005/978b9956-81f8-41ae-a3f1-7c14bbc00843)

### *Passo 3: Inicialização da Máquina Virtual*
- Após a importação, selecione a máquina virtual importada na lista de máquinas virtuais do VirtualBox.
- Clique em “Iniciar” para inicializar a máquina virtual.

## Configuração Kafka

### *Passo 1: Iniciando o Servidor Kafka*
Para executar essa etapa, iremos executar o comando abaixo:
```shell 
sudo /home/puc/kafka_2.11-1.0.0/bin/kafka-server-start.sh /home/puc/kafka_2.11-1.0.0/config/server.properties
```
Vamos entender melhor esse comando:
- **sudo**: Executa o comando com privilégios de superusuário (root). Isso é necessário se o Kafka precisar acessar arquivos ou portas que requerem permissões elevadas.
- **/home/puc/kafka_2.11-1.0.0/bin/kafka-server-start.sh**: Este é o script de shell fornecido pelo Kafka para iniciar o servidor Kafka. O script está localizado no diretório de instalação do Kafka (/home/puc/kafka_2.11-1.0.0/bin).
- **/home/puc/kafka_2.11-1.0.0/config/server.properties**: Este é o arquivo de configuração que o Kafka usa para inicializar o servidor. O arquivo server.properties contém várias configurações necessárias para o funcionamento do servidor Kafka, como: <br>
  - Portas de rede <br>
  - Diretórios de log <br>
  - Configurações de replicação <br>
  - Configurações de zookeeper
  
![image](https://github.com/ErickBrenno/Kafka-Flume/assets/83048005/ae08b414-6103-40c9-9fbe-df02c28279d8)
> NOTA: O comando sudo, solicita a senha do usuário root.

### *Passo 2: Criando Tópicos*
Para executar essa etapa, iremos executar o comando abaixo:
```shell
sudo /home/puc/kafka_2.11-1.0.0/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1  --partitions 1 --topic aula1006
```
Vamos entender melhor esse comando:
- **sudo**: Executa o comando com privilégios de superusuário (root). Isso é necessário se o Kafka precisar acessar arquivos ou portas que requerem permissões elevadas.

- **/home/puc/kafka_2.11-1.0.0/bin/kafka-topics.sh**: Este é o script de shell fornecido pelo Kafka para gerenciar tópicos. O script está localizado no diretório de instalação do Kafka (/home/puc/kafka_2.11-1.0.0/bin)

- **--create**: Especifica que você deseja criar um novo tópico.

- **--zookeeper localhost:2181**: Especifica o endereço do servidor Zookeeper que o Kafka usará para gerenciar metadados de tópicos. localhost é o endereço do servidor Zookeeper (neste caso, está rodando localmente) e 2181 é a porta padrão onde o Zookeeper está escutando.
- **--replication-factor 1**: Define o fator de replicação do tópico. Neste caso, o fator de replicação é 1, o que significa que cada partição do tópico terá uma única réplica (nenhuma redundância).
  
- **--partitions 1**: Define o número de partições para o tópico. Neste caso, o tópico terá 1 partição.
  
- **--topic aula1006**: Define o nome do tópico a ser criado. Neste caso, o nome do tópico é aula1006.

![image](https://github.com/ErickBrenno/Kafka-Flume/assets/83048005/53ac29f8-225f-4c74-a6e9-8c546d5f9d44)

> Podemos Executar o comando abaixo para listarmos os tópicos existentes <br>
> ```shell sudo /home/puc/kafka_2.11-1.0.0/bin/kafka-topics.sh --list --zookeeper localhost:2181 ```

## Producer e Consumer

### Confugurando Producer
Um producer no Kafka é um componente que publica (envia) dados para tópicos no cluster Kafka, atuando como a fonte de dados para o sistema de mensagens.
Para criarmos um Producer no tópico que criarmos, iremos executar o seguinte comando:
```shell sudo /home/puc/kafka_2.11-1.0.0/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic aula1006```
Vamos entender melhor esse comando:
- **sudo**: Executa o comando com privilégios de superusuário (root). Isso é necessário se o Kafka precisar acessar arquivos ou portas que requerem permissões elevadas.
- 

### Configurando Consumer
Um consumer no Kafka é um componente que lê (consome) dados de tópicos no cluster Kafka, processando ou utilizando esses dados conforme necessário.
