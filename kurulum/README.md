# Apache Airflow Docker Üzerinde Kurulum Komutları

## Hazırlık:
```bash
mkdir airflow-docker
cd airflow-docker
mkdir logs\mkdir dags
mkdir plugins
```

## Dockerfile, `docker-compose.yaml` ve `requirements.txt` dosyaları `airflow-docker` klasörü içine kopyalanır.

## Docker imajını oluşturmak için:
```bash
docker build . --tag "airflow-v2"
```

## Docker imajlarından container oluşturmak için:
```bash
docker-compose up -d
```

## Docker imajlarının terminal ekranlarına bağlanmak için:
```bash
docker exec -it airflow-worker /bin/bash
```

### `apache-airflow-providers-microsoft-mssql` provider paketinin doğru kurulup kurulmadığının kontrolü için:
1. Yukarıdaki komut ile container terminal ekranına bağlanılır.
2. Aşağıdaki komut çalıştırılır:
```bash
ls /home/airflow/.local/lib/python3.12/site-packages/airflow/providers/microsoft/mssql/
```
3. Eğer `hooks` ve `operators` klasörleri varsa, `apache-airflow-providers-microsoft-mssql` provider doğru şekilde kurulmuş ve çalışıyordur.
4. `exit` komutu ile container terminalinden çıkış yapılabilir.

## Docker container ve volume silmek için:
```bash
docker-compose down --volumes
```

## Docker container yeniden başlatmak için:
```bash
docker-compose restart
