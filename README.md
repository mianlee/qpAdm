## qpWave/qpAdm for NorthEast project

Which population are the likely sources of their ancestry or how
much ancestry they can trace to each of them.

### qpWave/qpAdm framework
**Left population set:** *Target/Test* populations (whose history of admixture we are investigating) and *Reference* populations（potential sources of ancestry).


**Reight population set:** A set of *Outgroups*.

It requires a set of outgroup populations that contain enough genetic variation
to be informative on the relationships between reference and target populations, but to have had no recent gene flow from reference
or target populations.


This methodology allows one to model the *Target/Test* population as an *N-way* mixture of the *Reference* populations by exploiting the fact that the *Reference* populations differ in their relationship to the *outgroups*.

qpWave/qpAdm was used to model individuals from **Northeast Asia (NEs)** as mixtures of ancestry related to one, two, or three different sources. This method relies on comparing the relationship each set of *target/test* and sources share with a set of outgroups, without requiring explicit description of the exact phylogenetic relationship shared between the outgroups.

We first model ancient populations as having ancestry from N=1, 2, 3 other populations.


### NE20 Individuals (29,060 years old)

**One-way mixture:**

Left = (NE20, *Ref*)

**Ref:**
Yana1,
Yana2,
Malta1,
UstBelaya_N,
Tianyuan,
DevilsCave_N,
Kolyma,
Clovis,
USR1,
HDYM1,
Bbdong,
Qihe,
Chokhopani,
Mebrak,
Ikawazu,
Oroqen,
Han,
Ami,
Itelman,
Aleut,
Pima,
Mayan,
Mixtec,
Mixe,
Zapotec,
Piapoco,
Karitiana,
Surui,
Quechua,
Chane,
NE56,
NE_12K,
NE-5,
NE-1,
NE_10K,
NE_9k,
NE_9K,
NE-45,
NE-35,
NE-16,
NE-49,
NE_7K,
NE_6K,
NE-22,
NE_5.5K,
NE-59.


Right = (Mota, UstIshim, Kostenki14, GoyetQ116-1, Vestonice16, ElMiron, Villabruna, Stuttgart, Karelia, Loschbour, Satsurblia, Mbuti, French), [Melinda A. Yang et.al.,2016](https://www.cell.com/current-biology/pdfExtended/S0960-9822(17)31195-8).


```
for i in `cat left_pop`; do echo NE20 $i | tr " " "\n" > $i; sed 's/XX/'${i}'/g' par > par.$i; done
```


```
for i in `cat left_pop`; do qsub qpAdm.sh -N $i -F $i ; done &
```

```
grep -A 1 "tail prob"   *.out |awk '{if ($6>0.05) print }'  |grep -v fixed | awk '{print $1}' |cut -f 2,3 -d "." | sed 's/.out-//g' | sort -u
```

**Try more references (NE20 as source):**

Left = (NE20, Ref) or (Ref, NE20)

**Ref:** Malta1, AfontovaGora3, Yana1, Yamnaya, Shamanka_EN, Lokomotiv_EN, UstBelaya_N, UstBelaya_MED, UstBelaya_EBA, Afanasievo, Andronovo, Boisman_MN, DevilsCave_N, Kolyma, Clovis, USR1, Saqqaq, HDYM1, Bbdong, Qihe, Chokhopani, Mebrak, Ikawazu, Altaian, Oroqen, Chukchi, Itelman, Aleut, Koryak, Japanese, Korean, Han, Miao, Ami, Lahu, Onge, Papuan, Pima, Mayan, Mixtec, Mixe, Zapotec, Piapoco, Karitiana, Surui, Quechua, Chane, NE20, NE_12K, NE-5, NE-1, NE_10K, NE_9k, NE_9K, NE-45, NE-35, NE-16, NE-49, NE_7K, NE_6K, NE-22, NE_5.5K, NE-59.

Right = (Mbuti, Yoruba, Mota, Onge, Papuan, Ust’-Ishim, Kostenki14, GoyetQ116-1, Vestonice16, sunghir , Satsurblia), [Martin Sikora et.al., Nature, 2019](https://www.nature.com/articles/s41586-019-1279-z).


```
for i in `cat left_pop`; do echo $i NE20 | tr " " "\n" > $i; sed 's/XX/'${i}'/g' par > par.$i; done

```


```
for i in `cat left_pop`; do qsub qpAdm.sh -N $i -F $i ; done &
```


```
grep -A 1 "tail prob"   *.out |awk '{if ($6>0.05) print }'  |grep -v fixed | awk '{print $1}' |cut -f 2,3 -d "." | sed 's/.out-//g' | sort -u
```

**Try different outgoups**

Mota, Ust’-Ishim, Kostenki14, GoyetQ116-1, Vestonice16, ElMiron, Villabruna, Stuttgart, Mbuti, French


**Two-way mixture:**

Left = (NE20, Ref1, Ref2)

**Ref:** Malta1,
AfontovaGora3,
Yana1,
Yamnaya,
Shamanka_EN,
Lokomotiv_EN,
UstBelaya_N,
UstBelaya_MED,
UstBelaya_EBA,
Afanasievo,
Andronovo,
Boisman_MN,
DevilsCave_N,
Kolyma,
Clovis,
USR1,
Saqqaq,
HDYM1,
Bbdong,
Qihe,
Chokhopani,
Mebrak,
Ikawazu,
Altaian,
Oroqen,
Chukchi,
Itelman,
Aleut,
Koryak,
Japanese,
Korean,
Han,
Miao,
Ami,
Lahu,
Onge,
Papuan,
Pima,
Mayan,
Mixtec,
Mixe,
Zapotec,
Piapoco,
Karitiana,
Surui,
Quechua,
Chane,
NE56,
NE_12K,
NE-5,
NE-1,
NE_10K,
NE_9k,
NE_9K,
NE-45,
NE-35,
NE-16,
NE-49,
NE_7K,
NE_6K,
NE-22,
NE_5.5K,
NE-59.

Right = (Mbuti, Yoruba, Mota, Onge, Papuan, Ust’-Ishim, Kostenki14, GoyetQ116-1, Vestonice16, sunghir , Satsurblia), [Martin Sikora et.al., Nature, 2019](https://www.nature.com/articles/s41586-019-1279-z).


```
for i in `cat left_pop`; do awk -v var=$i '{print var " " $1}' left_pop | grep -v "$i $i" >> 2way_list; done
```


```
for i in `cat 2way_list| tr " " "." `;do ( echo $i | tr "." "\n"; echo NE20 ; ) > $i; sed 's/XX/'${i}'/g' par > par.$i; done

```


```
for i in `cat 2way_list | tr " " "."`; do qsub qpAdm2.sh -N $i -F $i; done &
```

```
grep -A 3 "tail prob"   *.out |awk '{if ($6>0.05) print }'  |grep -v 'fixed\|infeasible' | awk '{print $1}' |cut -f 2,3 -d "." | sort -u > list.final
```


### NE56 Individuals (16,090 years old)

**One-way mixture:**

Left = (NE56, Ref) or (Ref, NE56)

**Ref:** Malta1, AfontovaGora3, Yana1, Yamnaya, Shamanka_EN, Lokomotiv_EN, UstBelaya_N, UstBelaya_MED, UstBelaya_EBA, Afanasievo, Andronovo, Boisman_MN, DevilsCave_N, Kolyma, Clovis, USR1, Saqqaq, HDYM1, Bbdong, Qihe, Chokhopani, Mebrak, Ikawazu, Altaian, Oroqen, Chukchi, Itelman, Aleut, Koryak, Japanese, Korean, Han, Miao, Ami, Lahu, Onge, Papuan, Pima, Mayan, Mixtec, Mixe, Zapotec, Piapoco, Karitiana, Surui, Quechua, Chane, NE20, NE_12K, NE-5, NE-1, NE_10K, NE_9k, NE_9K, NE-45, NE-35, NE-16, NE-49, NE_7K, NE_6K, NE-22, NE_5.5K, NE-59.

Right = (Mbuti, Yoruba, Mota, Onge, Papuan, Ust’-Ishim, Kostenki14, GoyetQ116-1, Vestonice16, sunghir , Satsurblia), [Martin Sikora et.al., Nature, 2019](https://www.nature.com/articles/s41586-019-1279-z).



```
for i in `cat left_pop`; do echo $i NE56 | tr " " "\n" > $i; sed 's/XX/'${i}'/g' par > par.$i; done
```


```
for i in `cat left_pop`; do qsub qpAdm.sh -N $i -F $i ; done &
```

```
grep -A 1 "tail prob"   *.out |awk '{if ($6>0.05) print }'  |grep -v fixed | awk '{print $1}' |cut -f 2,3 -d "." | sed 's/.out-//g' | sort -u > list.final
```


**Two-way mixture:**

Left = (NE56, Ref) or (Ref, NE56)

**Ref:** Malta1, AfontovaGora3, Yana1, Yamnaya, Shamanka_EN, Lokomotiv_EN, UstBelaya_N, UstBelaya_MED, UstBelaya_EBA, Afanasievo, Andronovo, Boisman_MN, DevilsCave_N, Kolyma, Clovis, USR1, Saqqaq, HDYM1, Bbdong, Qihe, Chokhopani, Mebrak, Ikawazu, Altaian, Oroqen, Chukchi, Itelman, Aleut, Koryak, Japanese, Korean, Han, Miao, Ami, Lahu, Onge, Papuan, Pima, Mayan, Mixtec, Mixe, Zapotec, Piapoco, Karitiana, Surui, Quechua, Chane, NE20, NE_12K, NE-5, NE-1, NE_10K, NE_9k, NE_9K, NE-45, NE-35, NE-16, NE-49, NE_7K, NE_6K, NE-22, NE_5.5K, NE-59.

Right = (Mbuti, Yoruba, Mota, Onge, Papuan, Ust’-Ishim, Kostenki14, GoyetQ116-1, Vestonice16, sunghir , Satsurblia), [Martin Sikora et.al., Nature, 2019](https://www.nature.com/articles/s41586-019-1279-z).

```
for i in `cat left_pop`; do awk -v var=$i '{print var " " $1}' left_pop | grep -v "$i $i" >> 2way_list; done
```


```
for i in `cat 2way_list| tr " " "." `;do ( echo $i | tr "." "\n"; echo NE56 ; ) > $i; sed 's/XX/'${i}'/g' par > par.$i; done

```


```
for i in `cat 2way_list | tr " " "."`; do qsub qpAdm2.sh -N $i -F $i; done &
```


```
grep -A 3 "tail prob"   *.out |awk '{if ($6>0.05) print }'  |grep -v 'fixed\|infeasible' | awk '{print $1}' |cut -f 2,3 -d "." | sort -u > list.final
```

### NE_12K Individuals (12,395 years old)

**One-way mixture:**

Left = (NE_12K, Ref) or (Ref, NE_12K)

**Ref:** Malta1, AfontovaGora3, Yana1, Yamnaya, Shamanka_EN, Lokomotiv_EN, UstBelaya_N, UstBelaya_MED, UstBelaya_EBA, Afanasievo, Andronovo, Boisman_MN, DevilsCave_N, Kolyma, Clovis, USR1, Saqqaq, HDYM1, Bbdong, Qihe, Chokhopani, Mebrak, Ikawazu, Altaian, Oroqen, Chukchi, Itelman, Aleut, Koryak, Japanese, Korean, Han, Miao, Ami, Lahu, Onge, Papuan, Pima, Mayan, Mixtec, Mixe, Zapotec, Piapoco, Karitiana, Surui, Quechua, Chane, NE20, NE56, NE-5, NE-1, NE_10K, NE_9k, NE_9K, NE-45, NE-35, NE-16, NE-49, NE_7K, NE_6K, NE-22, NE_5.5K, NE-59.

Right = (Mbuti, Yoruba, Mota, Onge, Papuan, Ust’-Ishim, Kostenki14, GoyetQ116-1, Vestonice16, sunghir , Satsurblia), [Martin Sikora et.al., Nature, 2019](https://www.nature.com/articles/s41586-019-1279-z).



```
for i in `cat left_pop`; do echo $i NE_12K | tr " " "\n" > $i; sed 's/XX/'${i}'/g' par > par.$i; done
```


```
for i in `cat left_pop`; do qsub qpAdm.sh -N $i -F $i ; done &
```

```
grep -A 1 "tail prob"   *.out |awk '{if ($6>0.05) print }'  |grep -v fixed | awk '{print $1}' |cut -f 2,3 -d "." | sed 's/.out-//g' | sort -u
```

**Two-way mixture:**

Left = (NE_12K, Ref) or (Ref, NE_12K)

**Ref:** Malta1, AfontovaGora3, Yana1, Yamnaya, Shamanka_EN, Lokomotiv_EN, UstBelaya_N, UstBelaya_MED, UstBelaya_EBA, Afanasievo, Andronovo, Boisman_MN, DevilsCave_N, Kolyma, Clovis, USR1, Saqqaq, HDYM1, Bbdong, Qihe, Chokhopani, Mebrak, Ikawazu, Altaian, Oroqen, Chukchi, Itelman, Aleut, Koryak, Japanese, Korean, Han, Miao, Ami, Lahu, Onge, Papuan, Pima, Mayan, Mixtec, Mixe, Zapotec, Piapoco, Karitiana, Surui, Quechua, Chane, NE20, NE56, NE-5, NE-1, NE_10K, NE_9k, NE_9K, NE-45, NE-35, NE-16, NE-49, NE_7K, NE_6K, NE-22, NE_5.5K, NE-59.

Right = (Mbuti, Yoruba, Mota, Onge, Papuan, Ust’-Ishim, Kostenki14, GoyetQ116-1, Vestonice16, sunghir , Satsurblia), [Martin Sikora et.al., Nature, 2019](https://www.nature.com/articles/s41586-019-1279-z).




```
for i in `cat left_pop`; do awk -v var=$i '{print var " " $1}' left_pop | grep -v "$i $i" >> 2way_list; done
```


```
for i in `cat 2way_list| tr " " "." `;do ( echo $i | tr "." "\n"; echo NE_12K ; ) > $i; sed 's/XX/'${i}'/g' par > par.$i; done

```


```
for i in `cat 2way_list | tr " " "."`; do qsub qpAdm2.sh -N $i -F $i; done &
```

```
grep -A 3 "tail prob"   *.out |awk '{if ($6>0.05) print }'  |grep -v 'fixed\|infeasible' | awk '{print $1}' |cut -f 2,3 -d "." | sort -u > list.final
```
