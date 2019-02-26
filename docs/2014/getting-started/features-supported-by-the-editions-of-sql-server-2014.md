---
title: Funzionalità supportate dalle edizioni di SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- data-quality-services
- database-engine
- integration-services
- master-data-services
- reporting-services-native
- reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0652a2545f0b1e9d591777f0bcabe6395cf4feaa
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/25/2019
ms.locfileid: "56802655"
---
# <a name="features-supported-by-the-editions-of-sql-server-2014"></a>Funzionalità supportate dalle edizioni di SQL Server 2014


  In questo argomento vengono forniti i dettagli delle funzionalità supportate dalle diverse edizioni di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. 

 > **Nota:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è disponibile in versione di valutazione per un periodo di valutazione di 180 giorni. Per altre informazioni, vedere la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [sito Web Software di prova](https://go.microsoft.com/fwlink/?LinkId=190955).  
> 
> **NOTA:** Per le funzionalità supportate dalle edizioni Evaluation e Developer, vedere il set di funzionalità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition.  
  
 Per passare alla tabella per una tecnologia [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , fare clic sul relativo collegamento:  
  
 [Limiti di scalabilità tra prodotti](#CrossBoxScale)  
  
 [Disponibilità elevata](#High_availability)  
  
 [Scalabilità e prestazioni](#Scalability)  
  
 [Sicurezza](#Enterprise_security)  
  
 [Replica](#Replication)  
  
 [Strumenti di gestione](#Mgmt_Tools)  
  
 [Gestione RDBMS](#RDBMS_mgmt)  
  
 [Strumenti di sviluppo](#Dev_tools)  
  
 [Programmabilità](#Programmability)  
  
 [Integration Services](#SSIS)  
  
 [Integration Services adattatori avanzati](#SSIS_AA)  
  
 [Integration Services trasformazioni avanzate](#SSIS_AT)  
  
 [Master Data Services](#MDS)  
  
 [Data warehouse](#Data_warehouse)  
  
 [Analysis Services](#SSAS)  
  
 [BI Semantic Model (multidimensionale)](#BISemModel_multi)  
  
 [BI Semantic Model (tabulare)](#BISemModel_tabular)  
  
 [PowerPivot per SharePoint 2013](#PowerPivot)  
  
 [Data mining](#DataMining)  
  
 [Reporting Services](#Reporting)  
  
 [Client di Business Intelligence](#BIClients)  
  
 [Spaziali e i servizi di posizione](#Spatial)  
  
 [Servizi di Database aggiuntivi](#Add_DBServices)  
  
 [Altri componenti](#Other_Components)  
  
##  <a name="CrossBoxScale"></a> Limiti di scalabilità tra prodotti  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Capacità di calcolo massima usata da una singola istanza ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] motore di Database)<sup>1</sup>|Valore massimo del sistema operativo|Limitato a meno di 4 socket o 16 core|Limitato a meno di 4 socket o 16 core|Limitato a meno di 4 socket o 16 core|Limitato a meno di 1 socket o 4 core|Limitato a meno di 1 socket o 4 core|Limitato a meno di 1 socket o 4 core|  
|Capacità di calcolo massima usata da una singola istanza (Analysis Services, Reporting Services) <sup>1</sup>|Valore massimo del sistema operativo|Valore massimo del sistema operativo|Limitato a meno di 4 socket o 16 core|Limitato a meno di 4 socket o 16 core|Limitato a meno di 1 socket o 4 core|Limitato a meno di 1 socket o 4 core|Limitato a meno di 1 socket o 4 core|  
|Memoria massima usata (per ogni istanza del motore di database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] )|Valore massimo del sistema operativo|128 GB|128 GB|64 GB|1 GB|1 GB|1 GB|  
|Memoria massima usata (per ogni istanza [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)])|Valore massimo del sistema operativo|Valore massimo del sistema operativo|64 GB|N/D|N/D|N/D|N/D|  
|Memoria massima usata (per ogni istanza [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)])|Valore massimo del sistema operativo|Valore massimo del sistema operativo|64 GB|64 GB|4 GB|N/D|N/D|  
|Dimensione massima del database relazionale|524 PB|524 PB|524 PB|524 PB|10 GB|10 GB|10 GB|  
  
 <sup>1</sup> Enterprise Edition con Server + CAL Client Access License () basati su licenza (non disponibile per nuovi contratti) è limitata a un massimo di 20 core per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] istanza. Non sono previsti limiti nel modello di licenza server basato su core. Per altre informazioni, vedere [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
##  <a name="High_availability"></a> Disponibilità elevata  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Supporto di Server Core<sup>1</sup>|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Log Shipping|Yes|Yes|Yes|Yes||||  
|Mirroring del database|Yes|Sì (solo protezione FULL)|Sì (solo protezione FULL)|Solo server di controllo|Solo server di controllo|Solo server di controllo|Solo server di controllo|  
|Compressione backup|Yes|Yes|Yes|||||  
|Snapshot del database|Yes|||||||  
|Istanze del cluster di failover AlwaysOn|Sì (supporto del nodo: Valore massimo del sistema operativo|Sì (supporto del nodo: 2)|Sì (supporto del nodo: 2)|||||  
|Gruppi di disponibilità AlwaysOn|Sì (fino a 8 repliche secondarie, incluse 2 repliche secondarie sincrone)|||||||  
|Connection Director|Yes|||||||  
|Ripristino di pagine e file online|Yes|||||||  
|Indicizzazione online|Yes|||||||  
|Modifica dello schema online|Yes|||||||  
|Recupero rapido|Yes|||||||  
|Backup con mirroring|Yes|||||||  
|Aggiunta a caldo di CPU e memoria<sup>2</sup>|Yes|||||||  
|Database Recovery Advisor|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Backup crittografato|Yes|Yes|Yes|||||  
|Backup intelligente|Yes|Yes|Yes|No||||  
  
 <sup>1</sup>per altre informazioni sull'installazione [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] in Server Core, vedere [installare SQL Server 2014 in Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md).  
  
 <sup>2</sup>questa funzionalità è disponibile solo per 64-bit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Scalability"></a> Scalabilità e prestazioni  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Supporto di più istanze|50|50|50|50|50|50|50|  
|Partizionamento di tabelle e indici|Yes|||||||  
|Compressione dati|Yes|||||||  
|Resource Governor|Yes|||||||  
|Parallelismo di tabelle delle partizioni|Yes|||||||  
|Più contenitori Filestream|Yes|||||||  
|Allocazione di una matrice di buffer e di memoria in pagine grandi con supporto NUMA|Yes|||||||  
|Estensione del Pool di buffer <sup>1</sup>|Yes|Yes|Yes|||||  
|Governance delle risorse di I/O|Yes|||||||  
|OLTP in memoria <sup>1</sup>|Yes|||||||  
|Durabilità posticipata|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
  
 <sup>1</sup> questa funzionalità è disponibile solo per 64-bit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Enterprise_security"></a> Sicurezza  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Controllo di base|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Controllo con granularità fine|Yes|||||||  
|Crittografia trasparente del database|Yes|||||||  
|Extensible Key Management|Yes|||||||  
|Ruoli definiti dall'utente|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Database indipendenti|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Crittografia per backup|Yes|Yes|Yes|||||  
  
##  <a name="Replication"></a> Replication  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Rilevamento modifiche di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Replica di tipo merge|Yes|Yes|Yes|Sì (solo sottoscrittore)|Sì (solo sottoscrittore)|Sì (solo sottoscrittore)|Sì (solo sottoscrittore)|  
|Replica transazionale|Yes|Yes|Yes|Sì (solo sottoscrittore)|Sì (solo sottoscrittore)|Sì (solo sottoscrittore)|Sì (solo sottoscrittore)|  
|Replica snapshot|Yes|Yes|Yes|Sì (solo sottoscrittore|Sì (solo sottoscrittore)|Sì (solo sottoscrittore)|Sì (solo sottoscrittore)|  
|Sottoscrittori eterogenei|Yes|Yes|Yes|||||  
|Pubblicazione Oracle|Yes|||||||  
|Replica transazionale peer-to-peer|Yes|||||||  
  
##  <a name="Mgmt_Tools"></a> Management Tools  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|SMO (SQL Management Objects)|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Gestione configurazione SQL Server|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|CMD SQL (strumento da riga di comando)|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio|Yes|Yes|Yes|Yes|Yes|Yes||  
|Riesecuzione distribuita - Strumento di amministrazione|Yes|Yes|Yes|Yes|Yes|Yes||  
|Distributed Replay - Client|Yes|No|Yes|Yes||||  
|Distributed Replay - Controller|Sì (Enterprise supporta fino a 16 client, Developer supporta solo 1 client)|No|Sì (supporto di 1 solo client)|Sì (supporto di 1 solo client)||||  
|SQL Profiler|Yes|Yes|Yes|No<sup>2</sup>|No<sup>2</sup>|No<sup>2</sup>|No<sup>2</sup>|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent|Yes|Yes|Yes|Yes||||  
|Management Pack di Microsoft System Center Operations Manager|Yes|Yes|Yes|Yes||||  
|Ottimizzazione guidata motore di database (DTA)|Yes|Yes|Sì <sup>3</sup>|Sì <sup>3</sup>||||  
|Procedura guidata Distribuire un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a una macchina virtuale di Windows Azure|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] File di dati in Microsoft Azure|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
  
 <sup>2</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] web, [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Tools e [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services può essere eseguito usando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition.  
  
 <sup>3</sup> ottimizzazione abilitata solo sulle funzionalità di Standard edition.  
  
##  <a name="RDBMS_mgmt"></a> RDBMS Manageability  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Istanze utente|||||Yes|Yes|Yes|  
|Database locale|||||Yes|Yes||  
|Connessione amministrativa dedicata|Yes|Yes|Yes|Yes|Sì (con flag di traccia)|Sì (con flag di traccia)|Sì (con flag di traccia)|  
|Supporto per script di PowerShell|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Supporto SysPrep<sup>1</sup>|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Supporto per le operazioni del componente dell'applicazione livello dati - estrazione, distribuzione, aggiornamento, eliminazione|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Automazione dei criteri (controllo pianificato e modifica)|Yes|Yes|Yes|Yes||||  
|Agente di raccolta dati relativi alle prestazioni|Yes|Yes|Yes|Yes||||  
|In grado di registrarsi come un'istanza gestita in una gestione a più istanze|Yes|Yes|Yes|Yes||||  
|Report di prestazioni standard|Yes|Yes|Yes|Yes||||  
|Guide di piano e blocco del piano per le guide di piano|Yes|Yes|Yes|Yes||||  
|Query diretta di viste indicizzate (tramite hint NOEXPAND)|Yes|Yes|Yes|Yes||||  
|Gestione automatica viste indicizzate|Yes|Yes|Yes|Yes||||  
|Viste partizionate distribuite|Yes|Parziale. Le viste partizionate distribuite non sono aggiornabili|Parziale. Le viste partizionate distribuite non sono aggiornabili|Parziale. Le viste partizionate distribuite non sono aggiornabili|Parziale. Le viste partizionate distribuite non sono aggiornabili|Parziale. Le viste partizionate distribuite non sono aggiornabili|Parziale. Le viste partizionate distribuite non sono aggiornabili|  
|Operazioni indicizzate parallele|Yes|||||||  
|Utilizzo automatico di viste indicizzate da Query Optimizer|Yes|||||||  
|Verifica di coerenza parallela|Yes|||||||  
|Punto di controllo dell'utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Yes|||||||  
|Database indipendenti|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Estensione del Pool di buffer<sup>2</sup>|Yes|Yes|Yes|||||  
  
 <sup>1</sup> Per altre informazioni, vedere [Considerazioni sull'installazione di SQL Server tramite SysPrep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
  
 <sup>2</sup> questa funzionalità è disponibile solo per 64-bit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Dev_tools"></a> Development Tools  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio Integration|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Intellisense ([!INCLUDE[tsql](../includes/tsql-md.md)] e MDX)|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Yes|Yes|Yes|Yes|Yes|||  
|Strumenti di progettazione e modifica di query SQL<sup>1</sup>|Yes|Yes|Yes|||||  
|Supporto controllo versione<sup>1</sup>|Yes|Yes|Yes|||||  
|Modifica MDX, eseguire il debug, strumenti di progettazione e<sup>1</sup>|Yes|Yes|Yes|||||  
  
 <sup>1</sup> questa funzionalità non è disponibile per la versione a 64 bit di Standard edition.  
  
##  <a name="Programmability"></a> Programmability  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integrazione con Common Language Runtime (CLR)|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Supporto XML nativo|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Indicizzazione XML|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Funzionalità MERGE e UPSERT|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Supporto FILESTREAM|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|FileTable|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Tipi di dati data e ora|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Supporto di internazionalizzazione|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Ricerca full-text e semantica|Yes|Yes|Yes|Yes|Yes|||  
|Impostazione della lingua nelle query|Yes|Yes|Yes|Yes|Yes|||  
|Service Broker (messaggistica)|Yes|Yes|Yes|No (solo client)|No (solo client)|No (solo client)|No (solo client)|  
|Endpoint [!INCLUDE[tsql](../includes/tsql-md.md)]|Yes|Yes|Yes|Yes||||  
  
##  <a name="SSIS"></a> Integration Services  
  
|Funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Connettori origine dati incorporati|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Progettazione SSIS e SSIS Runtime|Yes|Yes|Yes|||||  
|Trasformazioni di base|Yes|Yes|Yes|||||  
|Strumenti di profiling dei dati di base|Yes|Yes|Yes|||||  
|Servizio Change Data Capture per Oracle di Attunity|Yes|||||||  
|Progettazione Change Data Capture per Oracle di Attunity|Yes|||||||  
  
###  <a name="SSIS_AA"></a> Integration Services - Adattatori avanzati  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Destinazione Oracle a prestazioni elevate|Yes|||||||  
|Destinazione Teradata a prestazioni elevate|Yes|||||||  
|Origine e destinazione SAP BW|Yes|||||||  
|Adattatore di destinazione per il training del modello di data mining|Yes|||||||  
|Adattatore di destinazione dell'elaborazione dimensione|Yes|||||||  
|Adattatore di destinazione dell'elaborazione partizione|Yes|||||||  
|Componenti Change Data Capture di Attunity|Yes|||||||  
|Connettore per ODBC (Open Database Connectivity) di Attunity|Yes|||||||  
  
###  <a name="SSIS_AT"></a> Integration Services - Trasformazioni avanzate  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Ricerche persistenti (prestazioni elevate)|Yes|||||||  
|Trasformazione di query di data mining|Yes|||||||  
|Trasformazioni di Ricerca fuzzy e Raggruppamento fuzzy|Yes|||||||  
|Trasformazioni di estrazioni e ricerca termini|Yes|||||||  
  
##  <a name="MDS"></a> Master Data Services  
  
> [!NOTE]  
>  -   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] è disponibile solo nelle edizioni a 64 bit di Business Intelligence e Enterprise.  
  
|Funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|Yes|Yes||||||  
|Applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]|Yes|Yes||||||  
  
##  <a name="Data_warehouse"></a> Data Warehouse  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Creazione di cubi senza database|Yes|Yes|Yes|||||  
|Generazione automatica dello schema della gestione temporanea e del data warehouse|Yes|Yes|Yes|||||  
|Change Data Capture|Yes|||||||  
|Ottimizzazione query join a stella|Yes|||||||  
|Configurazione scalabile di Analysis Services di sola lettura|Yes|||||||  
|Elaborazione di query parallela su tabelle e indici partizionati|Yes|||||||  
|indici columnstore ottimizzati memoria xVelocity|Yes|||||||  
|Aggregazione batch globale|Yes|||||||  
  
##  <a name="SSAS"></a> Analysis Services  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Database condiviso scalabile (collegamento/scollegamento, database di sola lettura)|Yes|Yes||||||  
|Backup/ripristino, Collegamento/Scollegamento di database|Yes|Yes|Yes|||||  
|Sincronizzare database|Yes|Yes||||||  
|Disponibilità elevata|Yes|Yes|Yes|||||  
|Programmabilità (AMO, ADOMD.Net, OLEDB, XML/A, ASSL)|Yes|Yes|Yes|||||  
  
###  <a name="BISemModel_multi"></a> BI Semantic Model (multidimensionale)  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Misure semiadditive|Yes|Yes|No<sup>1</sup>|||||  
|Gerarchie|Yes|Yes|Yes|||||  
|KPI|Yes|Yes|Yes|||||  
|prospettive|Yes|Yes||||||  
|Azioni|Yes|Yes|Yes|||||  
|Funzionalità di Business Intelligence per la contabilità|Yes|Yes|Yes|||||  
|Business Intelligence per gerarchie temporali|Yes|Yes|Yes|||||  
|Rollup personalizzati|Yes|Yes|Yes|||||  
|Cubo writeback|Yes|Yes|Yes|||||  
|Dimensioni writeback|Yes|Yes||||||  
|Celle writeback|Yes|Yes|Yes|||||  
|Drill-through|Yes|Yes|Yes|||||  
|Tipi di gerarchia avanzati (padre-figlio, gerarchie incomplete)|Yes|Yes|Yes|||||  
|Dimensioni avanzate (dimensioni di riferimento, dimensioni molti-a-molti|Yes|Yes|Yes|||||  
|Dimensioni e misure collegate|Yes|Yes||||||  
|Traduzioni|Yes|Yes|Yes|||||  
|Aggregations|Yes|Yes|Yes|||||  
|Più partizioni|Yes|Yes|Sì, fino a 3|||||  
|Memorizzazione nella cache attiva|Yes|Yes||||||  
|Assembly personalizzati (procedure archiviate)|Yes|Yes|Yes|||||  
|Query e script MDX|Yes|Yes|Yes|||||  
|Query DAX|Yes|Yes||||||  
|Modello di sicurezza basato su ruoli|Yes|Yes|Yes|||||  
|Sicurezza a livello di cella e dimensione|Yes|Yes|Yes|||||  
|Archivio di stringhe scalabile|Yes|Yes|Yes|||||  
|MOLAP, ROLAP, modalità di archiviazione HOLAP|Yes|Yes|Yes|||||  
|Trasporto XML binario e compresso|Yes|Yes|Yes|||||  
|Elaborazione in modalità push|Yes|Yes||||||  
|Writeback diretto|Yes|Yes||||||  
|Espressioni di misura|Yes|Yes||||||  
  
 <sup>1</sup>misura semiadattiva LastChild the è supportata nell'edizione standard, ma altre misure semiadattive come None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren e ByAccount non lo sono. Le misure additive, ad esempio Sum, Count, Min, Max e quelle non additive (DistinctCount) sono supportate in tutte le edizioni.  
  
###  <a name="BISemModel_tabular"></a> BI Semantic Model (Tabular)  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Gerarchie|Yes|Yes||||||  
|KPI|Yes|Yes||||||  
|prospettive|Yes|Yes||||||  
|Traduzioni|Yes|Yes||||||  
|Calcoli DAX, query DAX, query MDX|Yes|Yes||||||  
|Sicurezza a livello di riga|Yes|Yes||||||  
|Partizioni|Yes|Yes||||||  
|Modalità di archiviazione In-Memory e DirectQuery (solo tabulare)|Yes|Yes||||||  
  
###  <a name="PowerPivot"></a> PowerPivot per SharePoint  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integrazione di farm SharePoint basata sull'architettura di servizi condivisi|Yes|Yes||||||  
|Report sull'utilizzo|Yes|Yes||||||  
|Regole di monitoraggio dell'integrità|Yes|Yes||||||  
|Raccolta PowerPivot|Yes|Yes||||||  
|Aggiornamento dei dati PowerPivot|Yes|Yes||||||  
|Feed di dati PowerPivot|Yes|Yes||||||  
  
###  <a name="DataMining"></a> Data Mining  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Algoritmi standard|Yes|Yes|Yes|||||  
|Strumenti di data mining (procedure guidate, editor, generatori di query)|Yes|Yes|Yes|||||  
|Convalida incrociata|Yes|Yes||||||  
|Modelli in base a subset filtrati dei dati della struttura di data mining|Yes|Yes||||||  
|Serie temporale: combinazione personalizzata tra metodi ARTXP e ARIMA|Yes|Yes||||||  
|Serie temporale: stima con nuovi dati|Yes|Yes||||||  
|Query di data mining simultanee illimitate|Yes|Yes||||||  
|Opzioni di configurazione e ottimizzazione avanzate per algoritmi di data mining|Yes|Yes||||||  
|Supporto per algoritmi plug-in|Yes|Yes||||||  
|Elaborazione parallela dei modelli|Yes|Yes||||||  
|Serie temporale: stima incrociata tra serie|Yes|Yes||||||  
|Attributi illimitati per Association Rules|Yes|Yes||||||  
|Stima basata su sequenze|Yes|Yes||||||  
|Più destinazioni di stima per gli algoritmi Logistic Regression, Neural Network e Naïve Bayes|Yes|Yes||||||  
  
##  <a name="Reporting"></a> Reporting Services  
  
###  <a name="Reporting_features"></a> Funzionalità di Reporting Services  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Edizione supportata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per il database del catalogo|Standard o versione successiva|Standard o versione successiva|Standard o versione successiva|Web|Express|||  
|Edizione supportata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per le origini dati|Tutte le edizioni di   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Tutte le edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Tutte le edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Web|Express|||  
|Server di report|Yes|Yes|Yes|Yes|Yes|||  
|Progettazione report|Yes|Yes|Yes|Yes|Yes|||  
|Gestione report|Yes|Yes|Yes|Yes|Yes|||  
|Sicurezza basata sui ruoli|Yes|Yes|Yes|Yes|Yes|||  
|Esportazione in Word e supporto formato RTF|Yes|Yes|Yes|Yes|Yes|||  
|Misuratori e grafici migliorati|Yes|Yes|Yes|Yes|Yes|||  
|Esportazione nei formati Excel, PDF e immagine|Yes|Yes|Yes|Yes|Yes|||  
|Autenticazione personalizzata|Yes|Yes|Yes|Yes|Yes|||  
|Dati del report come feed di dati|Yes|Yes|Yes|Yes|Yes|||  
|Supporto modelli|Yes|Yes|Yes|Yes||||  
|Creare ruoli personalizzati per la sicurezza basata sui ruoli|Yes|Yes|Yes|||||  
|Sicurezza elemento modello|Yes|Yes|Yes|||||  
|Click-through illimitato|Yes|Yes|Yes|||||  
|Libreria componenti condivisa|Yes|Yes|Yes|||||  
|Sottoscrizioni e pianificazione posta elettronica e condivisione file|Yes|Yes|Yes|||||  
|Cronologia report, esecuzione snapshot e memorizzazione nella cache|Yes|Yes|Yes|||||  
|Integrazione con SharePoint|Yes|Yes|Yes|||||  
|Supporto origini dati remote e non SQL<sup>1</sup>|Yes|Yes|Yes|||||  
|Estensibilità RDCE per il rendering, il recapito e le origini dati|Yes|Yes|Yes|||||  
|Sottoscrizione di report guidate dai dati|Yes|Yes||||||  
|Distribuzione con scalabilità orizzontale (Web farm)|Yes|Yes||||||  
|Avvisi<sup>2</sup>|Yes|Yes||||||  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] <sup>2</sup>|Yes|Yes||||||  
  
 <sup>1</sup>per altre informazioni su origini dati supportate nelle [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)], vedere [origini dati supportate da Reporting Services &#40;SSRS&#41;](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
 <sup>2</sup>richiede [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in modalità SharePoint. Per altre informazioni, vedere [installazione in modalità SharePoint di Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
### <a name="report-server-database-server-edition-requirements"></a>Requisiti dell'edizione server del database del server di report  
 Quando si crea un database del server di report, non tutte le edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] possono essere usate per ospitare il database. Nella tabella seguente sono illustrate le edizioni del [!INCLUDE[ssDE](../includes/ssde-md.md)] che è possibile usare per le edizioni specifiche di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
|Per questa edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services|Edizione dell'istanza del Motore di database da usare per ospitare il database|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Edizioni Standard, Business Intelligence Enterprise (locali o remote)|  
|Business Intelligence|Edizioni Standard, Business Intelligence Enterprise (locali o remote)|  
|Standard|Edizioni Standard, Enterprise (locali o remote)|  
|Web|Web Edition (solo locale)|  
|Express with Advanced Services|Express with Advanced Services (solo locale).|  
|Copia di valutazione|Copia di valutazione|  
  
##  <a name="BIClients"></a> Client di Business Intelligence  
 Le seguenti applicazioni client del software sono disponibili nell'Area download Microsoft e vengono fornite come supporto per la creazione di documenti di Business Intelligence eseguiti in un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Quando questi documenti vengono ospitati in un ambiente server, usare un'edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supportata per tale tipo di documento. Nella tabella seguente viene indicata l'edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contenente le funzionalità del server richieste per ospitare i documenti creati in queste applicazioni client.  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]|Yes|Yes|Yes|||||  
|Componenti aggiuntivi di data mining per Excel e Visio 2010|Yes|Yes|Yes|||||  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010|Yes|Yes||||||  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]|Yes|Yes||||||  
  
> [!NOTE]
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] è un componente aggiuntivo di Excel e non dipende da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Tuttavia [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] è richiesto per la condivisione e collaborazione con le cartelle di lavoro [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] in SharePoint e questa funzionalità è disponibile come parte delle edizioni [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise e Business Intelligence.  
> 2.  La tabella sopra riportata identifica le edizioni [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] richieste per abilitare gli strumenti client; tuttavia le funzionalità possono accedere ai dati ospitati in ogni edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Spatial"></a> Spatial and Location Services  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Indici spaziali|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Tipi di dati planari e geodetici|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Librerie spaziali avanzate|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Importazione/esportazione di formati di dati spaziali standard del settore|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
  
##  <a name="Add_DBServices"></a> Additional Database Services  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|Yes|Yes|Yes|Yes|Yes|Yes|Yes|  
|Posta elettronica database|Yes|Yes|Yes|Yes||||  
  
##  <a name="Other_Components"></a> Altri componenti  
  
|Nome funzionalità|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Data Quality Services|Yes|Yes||||||  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|StreamInsight Standard Edition||||  
|StreamInsight HA|StreamInsight Premium Edition|||||||  
  
## <a name="see-also"></a>Vedere anche  
 [Specifiche di prodotto per SQL Server 2014](../../2014/getting-started/sql-server-2014-product-specifications.md)   
 [Installazione di SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Guida introduttiva all'installazione di SQL Server 2014](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
