# Лабжурнал по Jupiter plot
- Работа в начале проводилась в юпитер ноутбуке, потом в командной строке, выходила постоянная ошибка (Error 137), что не хватает вычислительной мощности (что странно), поэтому было приняло решение переделать на сервере, где все уже прекрасно посчитлаось.

## 1.Загрузка геномов
- референс TAIR10.1, Arabidopsis thaliana
- для сравнения будем использовать другой вид: Arabidopsis halleri (ddAraHall_1.3)

```
- # GCF_000001735.4 (TAIR10.1)
wget -O tair10.fna.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/001/735/GCF_000001735.4_TAIR10.1/GCF_000001735.4_TAIR10.1_genomic.fna.gz

!gunzip /content/tait10.fna.gz

# GCA_964271285.1 (A.halleri)
wget -O hall.fna.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/964/271/285/GCA_964271285.1_ddAraHall_1.3/GCA_964271285.1_ddAraHall_1.3_genomic.fna.gz

gunzip hall.fna.gz
```
- Референс оставляем неизменным, а вот hall.fna, имеет очень много контиг, которые мы обрезаем, чтобы оставить только основные хромосомы. 
```
sed '26021511,2840350d' hall.fna > hall_trimmed.fna
```

## 2. Настройка окружения и загрузка необходимых инструментов 
```
conda create -n jp
source activate jp && conda install -c conda-forge -c bioconda jupiterplot minimap2 samtools
conda install -c conda-forge -c bioconda circos circos-tools
```
## 3. Построение графика:
```
jupiter name=tair_hall ref=tair10.fna fa=hall_trimmed.fna
```
- также сохраню для себя команду для скачивания файла с сервера на локальный компьтер в убунту:
```
scp -i ~/.ssh/id_rsa aanferova@77.234.216.99:/media/eternus1/nfs/projects/users/aanferova/comparative_genomics/hw3/tair_hall.svg /home/anastasia/tair_hall.svg
```
- ![jupiter_plot](https://github.com/user-attachments/assets/21e0cd47-5af4-42ba-b043-122677e4e3aa)
