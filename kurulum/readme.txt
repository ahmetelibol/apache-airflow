#Apache Airflow Docker Üzerinde Kurulum Komutları:

## Docker imajını oluşturmak için: 
docker build . --tag "airflow-v2"

## Docker imajlarından container oluşturmak için:
docker-compose up -d

## Docker imajlarının terminal ekranlarına bağlanmak için:
docker exec -it airflow-worker /bin/bash

### apache-airflow-providers-microsoft-mssql provider paketinin doğru kurulup kurulmadığının kontrolü için
### yukarıdaki komut ile container terminal ekranına bağlanılır ve "ls /home/airflow/.local/lib/python3.12/site-packages/airflow/providers/microsoft/mssql/" komutu çalıştırılır.
### Eğer hooks ve operators klasörleri varsa apache-airflow-providers-microsoft-mssql provider doğru şekilde kurulmuş ve çalışıyordur.

## Docker container ve volume silmek için:
docker-compose down --volumes

## Docker container yeniden başlatmak için:
docker-compose restart
