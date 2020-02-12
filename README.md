# Trimania Crawler

The Trimania is a organization that carry out sweepstakes in Santa Catarina state on Sundays and give prizes. 

I created this project to mount a dataset and to make studies in numbers and locations that it would answer questions like **What is the neighboorhood with more winners in Joinville?** or **What were the numbers most selected in last year?**.

## Start

Currently, this project runs only in localhost. To configure in your computer follow the steps below. 

a) Installing dependencies

```bash
$ composer install
```

b) Configure environment file

```bash
$ cp .env.default .env
```

c) Configure environment file

```bash
$ cp .env.default .env
```

d) Create a directory called `data_csv`

```bash
$ mkdir data_csv
```

e) You can use docker (I recommend)

```bash
$ docker-compose up -d
```

e) Import database

I like using the command line for that. Of course, you can to import the way you prefer. I let some databases in the *data directory*. 


```bash
mysql --host=172.17.0.1 -uroot -proot trimania < data/trimania_05_05_2018.sql
```

## Verify the containers

```bash
$ docker ps

CONTAINER ID        IMAGE
3efe06f79d2e        trimania-crawler_web    ...     
f1bbddbd9820        mysql                   ...
```

## Examples

To import or export data is necessary a __sweepstakes date__. Without this information will not possible run these functions. The date format is ```YYYY-MM-DD```.  

### Importing

To import data you need to run a command like below.
```bash
docker-compose exec web php web/index.php trimania:import --draw_date=2020-02-02
```
After the importation is showed the numbers and locations that were getting.

![Data Imported](imported.png)

### Exporting

To export data you need to run a command like below.

```bash
docker-compose exec web php web/index.php trimania:export --draw_year=2020  --type=numbers
docker-compose exec web php web/index.php trimania:export --draw_year=2020  --type=locations
```

The files will be gererated in `data_csv` directory.