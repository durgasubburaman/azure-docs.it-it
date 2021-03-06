<!-- A-series - compute-intensive instances, H-series -->

Le dimensioni delle serie A8-A11 e H sono note anche come *istanze a elevato uso di calcolo*. L'hardware che esegue queste dimensioni è progettato e ottimizzato per applicazioni a elevato utilizzo di calcolo e di rete, come applicazioni cluster HPC, modellazione e simulazioni. La serie A8-A11 usa Intel Xeon E5-2670 a 2,6 GHZ, mentre la serie H usa Intel Xeon E5-2667 v3 a 3,2 GHz. 

Le macchine virtuali serie H di Azure sono le VM high performance computing di prossima generazione che puntano a risolvere esigenze di calcolo di fascia alta, come modellazione molecolare e fluidodinamica computazionale. Queste VM a 8 e 16 core sono basate sulla tecnologia del processore Intel Haswell E5-2667 V3 con memoria DDR4 e archiviazione basata su SSD locale. 

Oltre alla sostanziale potenza della CPU, la serie H offre diverse opzioni per rete RDMA a bassa latenza con FDR InfiniBand e diverse configurazioni di memoria a supporto di requisiti di calcolo a elevato uso di memoria.



## <a name="h-series"></a>Serie H

ACU: 290-300

| Dimensione | Core CPU | Memoria: GiB | Unità SSD locale: GiB | Valore massimo per dischi di dati | Velocità effettiva del disco max: IOPS | Larghezza di banda della rete/scheda NIC max |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |56 |1000 |16 |16x500 |2/alta |
| Standard_H16 |16 |112 |2000 |32 |32x500 |4/molto alta |
| Standard_H8m |8 |112 |1000 |16 |16x500 |2/alta |
| Standard_H16m |16 |224 |2000 |32 |32x500 |4/molto alta |
| Standard_H16r* |16 |112 |2000 |32 |32x500 |4/molto alta |
| Standard_H16mr* |16 |224 |2000 |32 |32x500 |4/molto alta |

*Con supporto di RDMA

<br>



## <a name="a-series---compute-intensive-instances"></a>Serie A - Istanze a elevato utilizzo di calcolo

ACU: 225

| Dimensione | Core CPU | Memoria: GiB | Unità HDD locale: GiB | Valore massimo per dischi di dati | Velocità effettiva del disco di dati max: IOPS | Larghezza di banda della rete/scheda NIC max |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8* |8 |56 |382 |16 |16x500 |2/alta |
| Standard_A9* |16 |112 |382 |16 |16x500 |4/molto alta |
| Standard_A10 |8 |56 |382 |16 |16x500 |2/alta |
| Standard_A11 |16 |112 |382 |16 |16x500 |4/molto alta |

*Con supporto di RDMA

<br>



