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

![image](https://user-images.githubusercontent.com/114621114/193101806-5bd0263a-4901-4965-a679-8fbec88de54b.png)
![image](https://user-images.githubusercontent.com/114621114/193101887-3ec34d13-0440-4909-899c-cb625c5dd69f.png)
![image](https://user-images.githubusercontent.com/114621114/193101970-542dd206-786f-4260-b181-dd29ec46594c.png)
![image](https://user-images.githubusercontent.com/114621114/193102103-14ade78f-242f-499c-a6b2-268b8b09c126.png)
![image](https://user-images.githubusercontent.com/114621114/193102227-11270c37-d104-47cf-aff9-489c4caf78ab.png)

![image](https://user-images.githubusercontent.com/114621114/193102357-4a452a0c-b173-46a0-9fb1-e712d78a7079.png)
![image](https://user-images.githubusercontent.com/114621114/193102555-b057bc9b-a5ce-4205-961c-d913751fc030.png)
![image](https://user-images.githubusercontent.com/114621114/193102638-46bc579e-3fc4-4f5f-8eb8-c3663c37a7b2.png)
![image](https://user-images.githubusercontent.com/114621114/193102729-9685dd11-76a0-4a2a-98c1-93998705e8dd.png)
![image](https://user-images.githubusercontent.com/114621114/193102798-9a62b64b-caf2-4f46-8ba0-271ec3b2822e.png)

![image](https://user-images.githubusercontent.com/114621114/193102966-de40d68c-2b24-45fe-9e85-ee9f0f8435d3.png)
![image](https://user-images.githubusercontent.com/114621114/193103042-893d38ad-b3c7-4908-806b-6547213a23b3.png)
![image](https://user-images.githubusercontent.com/114621114/193103132-1e9fcc44-38a0-4ce3-b341-2e665fc9c254.png)
![image](https://user-images.githubusercontent.com/114621114/193103218-a040522d-4c47-4fc4-a6d5-d3bf8a344cc5.png)
![image](https://user-images.githubusercontent.com/114621114/193103309-58d04bab-f63a-479e-8971-75de36f7806d.png)

![image](https://user-images.githubusercontent.com/114621114/193103472-ec8aac2b-16b4-4fef-98b0-4a3cb8518934.png)
![image](https://user-images.githubusercontent.com/114621114/193103595-bd606fd8-c1fb-4dde-9672-b7416f426d14.png)
![image](https://user-images.githubusercontent.com/114621114/193103669-1301864f-0d3a-46e7-88cc-f08b23661ff9.png)
![image](https://user-images.githubusercontent.com/114621114/193103748-31befe29-77a9-4853-bb2d-30f681f7039a.png)
![image](https://user-images.githubusercontent.com/114621114/193103873-3fefa93e-e844-4470-afb4-ee08d69a3f03.png)

#### Отчёты multiQC
Для исходных чтений

![image](https://user-images.githubusercontent.com/114621114/193090652-27bffef3-3bde-49f2-acde-25f0e1ae6b37.png)
![image](https://user-images.githubusercontent.com/114621114/193090799-d9b35501-b798-424a-aa71-03922f4f8225.png)
![image](https://user-images.githubusercontent.com/114621114/193090922-9b4b98d1-d3ff-4269-b87a-3eab897cfe6e.png)
![image](https://user-images.githubusercontent.com/114621114/193091008-ae1fa4ca-f6b9-49a1-9a1d-730978252b05.png)
![image](https://user-images.githubusercontent.com/114621114/193091244-241638ba-3245-4caf-a567-ccb35ec07520.png)
![image](https://user-images.githubusercontent.com/114621114/193091350-9b2822a2-e585-46b0-bf99-0560971069a6.png)

Для подрезанных чтений

![image](https://user-images.githubusercontent.com/114621114/193104058-c773b1e8-e47f-417e-b061-c011c1ee0ffc.png)
![image](https://user-images.githubusercontent.com/114621114/193104872-351a7d2a-5b0f-451c-86aa-04b49b8c5a4b.png)
![image](https://user-images.githubusercontent.com/114621114/193104179-4b0bfd53-d759-4153-b1c2-7ea2a3bda37f.png)
![image](https://user-images.githubusercontent.com/114621114/193104377-a983cf33-fb31-40b4-a90d-e2814529008b.png)
![image](https://user-images.githubusercontent.com/114621114/193104559-7ec67c6d-1f28-46a9-ae4d-03a9ae8ccf14.png)
![image](https://user-images.githubusercontent.com/114621114/193104663-7f5f0991-f620-4eb9-b35f-7738c9d2c6f4.png)



#### Собраны контиги из подрезанных чтений типа paired-end с помощью программы platanus assemble.
```bash
platanus assemble -o Pxut -f pairedend1.fastq.trimmed pairedend2.fastq.trimmed 2> assemble.log
```
#### 
#### Собраны скаффолды из контигов и подрезанных чтений с помощью программы platanus scaffold.
```bash
platanus scaffold -o Pxut -c Pxut_contig.fa -b Pxut_contigBubble.fa -IP1 pairedend1.fastq.trimmed pairedend2.fastq.trimmed -OP2 matepair1.fastq.int_trimmed matepair2.fastq.int_trimmed 2> scaffold.log
```
#### 
#### Уменьшено количество гэпов с помощью программы platanus gap_close.
```bash
platanus gap_close -o Pxut -c Pxut_scaffold.fa -IP1 pairedend1.fastq.trimmed pairedend2.fastq.trimmed -OP2 matepair1.fastq.int_trimmed matepair2.fastq.int_trimmed 2> gapclose.log
```
#### Удалены подрезанные .fastq файлы.
```bash
rm pairedend1.fastq.trimmed
rm pairedend2.fastq.trimmed
rm matepair1.fastq.int_trimmed
rm matepair2.fastq.int_trimmed
```
####
