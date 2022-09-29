# hse22_hw1
Ксения Лапшина.
4 группа

## Обязательная часть

#### Созданы ссылки на рабочие файлы в PuTTY.
```bash
ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
```
#### С помощью команды seqtk случайно выбраны 5 миллионов чтений типа paired-end из файлов oil_R1.fastq, oil_R2.fastq и 1.5 миллиона чтений типа mate-pairs из файлов oilMP_S4_L001_R1_001.fastq, oilMP_S4_L001_R2_001.fastq, для параметра -s (random seed) использовано число 1114.
```bash
seqtk sample -s1114 oil_R1.fastq 5000000 > pairedend1.fastq
seqtk sample -s1114 oil_R2.fastq 5000000 > pairedend2.fastq
seqtk sample -s1114 oilMP_S4_L001_R1_001.fastq 1500000 > matepair1.fastq
seqtk sample -s1114 oilMP_S4_L001_R2_001.fastq 1500000 > matepair2.fastq
```
#### Оценено качество исходных чтений с помощью программ fastQC и multiQC и получена общая статистика по ним.
```bash
mkdir fastqc
ls pairedend1.fastq | xargs -P 4 -tI{} fastqc -o fastqc {}
ls pairedend2.fastq | xargs -P 4 -tI{} fastqc -o fastqc {}
ls matepair1.fastq | xargs -P 4 -tI{} fastqc -o fastqc {}
ls matepair2.fastq | xargs -P 4 -tI{} fastqc -o fastqc {}
mkdir multiqc
multiqc -o multiqc fastqc
```
#### Чтения подрезаны по качеству и удалены адаптеры с помощью программ platanus_trim и platanus_internal_trim.
```bash
platanus_trim pairedend*
platanus_internal_trim matepair*
```
#### Удалены исходные .fastq файлы, полученные с помощью программы seqtk.
```bash
rm pairedend1.fastq
rm pairedend2.fastq
rm matepair1.fastq
rm matepair2.fastq
```
#### Оценено качество исходных чтений с помощью программ fastQC и multiQC и получена общая статистика по ним.
```bash
mkdir fastqc_trimmed
ls pairedend1.fastq.trimmed | xargs -P 4 -tI{} fastqc -o fastqc_trimmed {}
ls pairedend2.fastq.trimmed | xargs -P 4 -tI{} fastqc -o fastqc_trimmed {}
ls matepair1.fastq.int_trimmed | xargs -P 4 -tI{} fastqc -o fastqc_trimmed {}
ls matepair2.fastq.int_trimmed | xargs -P 4 -tI{} fastqc -o fastqc_trimmed {}
mkdir multiqc_trimmed
multiqc -o multiqc_trimmed fastqc_trimmed
```



#### Отчёты fastQC
Для исходных чтений

![image](https://user-images.githubusercontent.com/114621114/193092271-9a5db5b0-62bd-45c6-8773-d5f1efbcadc9.png)
![image](https://user-images.githubusercontent.com/114621114/193092393-d637428f-841c-44ee-ab4d-02b5c4582082.png)
![image](https://user-images.githubusercontent.com/114621114/193092495-61d4106a-1437-41a7-8cbd-c77a6882505d.png)
![image](https://user-images.githubusercontent.com/114621114/193092636-eda56a32-dd33-4b03-9309-a6b9caf0f9b6.png)
![image](https://user-images.githubusercontent.com/114621114/193092969-6ea54a99-8cde-4a42-befa-e4b2934ad417.png)

![image](https://user-images.githubusercontent.com/114621114/193093292-0cbb8b1a-112d-4315-8bb5-c37954652c9f.png)
![image](https://user-images.githubusercontent.com/114621114/193093460-ea4dcb9d-a8aa-4230-9226-40d18665a9aa.png)
![image](https://user-images.githubusercontent.com/114621114/193093539-30e26520-53f4-4e84-b836-0111dd0a33c9.png)
![image](https://user-images.githubusercontent.com/114621114/193093612-7581598a-af81-4919-a36b-16d2b87dd3cb.png)
![image](https://user-images.githubusercontent.com/114621114/193094310-791e7e41-aeda-4972-9c49-8ab6128316ad.png)

![image](https://user-images.githubusercontent.com/114621114/193094654-c10846e4-497b-4c83-a1d7-ec90d2170460.png)
![image](https://user-images.githubusercontent.com/114621114/193095392-0dc4f404-17da-4c7a-90f7-898f7fbde2b8.png)
![image](https://user-images.githubusercontent.com/114621114/193095626-4d57dc27-ef31-48e3-8978-8378f7fc4bd4.png)
![image](https://user-images.githubusercontent.com/114621114/193095953-36ef4f9f-cb09-4500-84dd-af4d32bc7ec9.png)
![image](https://user-images.githubusercontent.com/114621114/193096325-2cccd5f6-0f9d-4fa1-be6c-04ee2693fa77.png)

![image](https://user-images.githubusercontent.com/114621114/193097785-65da0bc0-1a59-4e26-85e7-8bf9e1e6813a.png)
![image](https://user-images.githubusercontent.com/114621114/193098012-d83d8cad-7210-4194-9604-2f03021d9ee0.png)
![image](https://user-images.githubusercontent.com/114621114/193098194-c309c7d2-8d13-4b37-88b6-2361d2a01746.png)
![image](https://user-images.githubusercontent.com/114621114/193098349-ee8f52c2-9d34-4e25-b2ce-9e72227bb30f.png)
![image](https://user-images.githubusercontent.com/114621114/193098494-250b3fd6-2227-4530-9e91-d7e35faa46db.png)




Для подрезанных чтений





#### Отчёты multiQC
Для исходных чтений

![image](https://user-images.githubusercontent.com/114621114/193090652-27bffef3-3bde-49f2-acde-25f0e1ae6b37.png)
![image](https://user-images.githubusercontent.com/114621114/193090799-d9b35501-b798-424a-aa71-03922f4f8225.png)
![image](https://user-images.githubusercontent.com/114621114/193090922-9b4b98d1-d3ff-4269-b87a-3eab897cfe6e.png)
![image](https://user-images.githubusercontent.com/114621114/193091008-ae1fa4ca-f6b9-49a1-9a1d-730978252b05.png)
![image](https://user-images.githubusercontent.com/114621114/193091244-241638ba-3245-4caf-a567-ccb35ec07520.png)
![image](https://user-images.githubusercontent.com/114621114/193091350-9b2822a2-e585-46b0-bf99-0560971069a6.png)

Для подрезанных чтений


