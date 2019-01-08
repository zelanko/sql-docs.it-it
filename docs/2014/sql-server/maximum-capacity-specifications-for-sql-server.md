---
title: Specifiche di capacità massima per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- objects [SQL Server]
- number capacity specifications [SQL Server]
- size [SQL Server], capacity specifications
- number of objects
- capacity specifications [SQL Server]
- maximum capacity specifications [SQL Server]
- size [SQL Server]
- replication capacity specifications [SQL Server]
- objects [SQL Server], capacity specifications
- Database Engine [SQL Server], capacity specifications
ms.assetid: 13e95046-0e76-4604-b561-d1a74dd824d7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 49e86c8b47a3a0de48a0138d96cec22d585901c6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771773"
---
# <a name="maximum-capacity-specifications-for-sql-server"></a>Specifiche di capacità massima per SQL Server
  Nelle tabelle seguenti vengono indicati le dimensioni e i numeri massimi dei diversi oggetti definiti nei componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per passare alla tabella per una tecnologia [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , fare clic sul relativo collegamento:  
  
 [Oggetti Motore di database di SQL Server](#Engine)  
  
 [Oggetti di Utilità SQL Server](#Utility)  
  
 [Oggetti applicazione livello dati di SQL Server](#DAC)  
  
 [Oggetti di replica di SQL Server](#Replication)  
  
##  <a name="Engine"></a> [!INCLUDE[ssDE](../includes/ssde-md.md)] Oggetti  
 Nella tabella seguente vengono indicati le dimensioni e i numeri massimi dei diversi oggetti definiti nei database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o a cui si fa riferimento nelle istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] oggetto|Quantità/dimensioni massime [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bit)|Quantità/dimensioni massime [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bit)|  
|---------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Dimensioni batch<br /><br /> Nota: Dimensioni pacchetto di rete corrisponde alle dimensioni dei pacchetti del flusso TDS (Tabular Data Stream) usati per le comunicazioni tra applicazioni e [!INCLUDE[ssDE](../includes/ssde-md.md)]relazionale. La dimensione predefinita del pacchetto è 4 KB e viene controllata dall'opzione di configurazione delle dimensioni del pacchetto di rete.|65.536 * dimensioni del pacchetto di rete|65.536 * dimensioni del pacchetto di rete|  
|Byte per ogni colonna di stringhe brevi|8.000|8.000|  
|Byte per ogni clausola GROUP BY, ORDER BY|8.060|8.060|  
|Byte per ogni chiave di indice<br /><br /> Nota: Il numero massimo di byte in una chiave di indice non può superare i 900 in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. È possibile definire una chiave utilizzando colonne di lunghezza variabile le cui dimensioni massime sono maggiori di 900, a condizione che non vengano inserite nelle colonne righe con più di 900 byte di dati. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è possibile includere in un indice non cluster colonne non chiave per evitare di raggiungere la dimensione massima di 900 byte consentita per le chiavi di indice.|900|900|  
|Byte per ogni chiave esterna|900|900|  
|Byte per ogni chiave primaria|900|900|  
|Byte per ogni riga<br /><br /> Nota:<br />        [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta l'archiviazione dei dati di overflow della riga che consente di spostare le colonne di lunghezza variabile all'esterno delle righe. Solo una radice di 24 byte viene archiviata nel record principale per le colonne di lunghezza variabile spostate all'esterno di righe. Di conseguenza, il limite delle righe effettivo è maggiore di quello delle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere l'argomento "Dati di overflow della riga che superano 8 KB" nella documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|8.060|8.060|  
|Byte per ogni riga nelle tabelle ottimizzate per la memoria<br /><br /> Nota:<br />        OLTP in memoria di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non supporta l'archiviazione dei dati di overflow della riga. Le colonne a lunghezza variabile non vengono spostate all'esterno delle righe. In questo modo viene limitata la larghezza massima delle colonne a lunghezza variabile che è possibile specificare in una tabella ottimizzata per la memoria alle dimensioni massime di riga. Per altre informazioni, vedere [Dimensioni di tabelle e righe per le tabelle con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md).|Non supportato|8.060|  
|Byte nel testo di origine di una stored procedure|Minore delle dimensioni batch o 250 MB|Minore delle dimensioni batch o 250 MB|  
|Byte per ogni colonna `varchar(max)`, `varbinary(max)`, `xml`, `text` o `image`|2^31-1|2^31-1|  
|Caratteri per ogni colonna `ntext` o `nvarchar(max)`|2^30-1|2^30-1|  
|Indici cluster per tabella|1|1|  
|Colonne in GROUP BY, ORDER BY|Limitato solo dal numero di byte|Limitato solo dal numero di byte|  
|Colonne o espressioni in un'istruzione GROUP BY WITH CUBE o WITH ROLLUP|10|10|  
|Colonne per ogni chiave di indice<br /><br /> Nota: Se la tabella contiene uno o più indici XML, la chiave di clustering della tabella utente viene limitata a 15 colonne perché la colonna XML viene aggiunta alla chiave di clustering dell'indice XML primario. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]è possibile includere in un indice non cluster colonne non chiave per evitare di raggiungere il limite massimo di 16 colonne chiave. Per altre informazioni, vedere [Creare indici con colonne incluse](../relational-databases/indexes/create-indexes-with-included-columns.md).|16|16|  
|Colonne per ogni chiave esterna|16|16|  
|Colonne per ogni chiave primaria|16|16|  
|Colonne per ogni tabella non estesa in larghezza|1.024|1.024|  
|Colonne per ogni tabella estesa in larghezza|30.000|30.000|  
|Colonne per ogni istruzione SELECT|4.096|4.096|  
|Colonne per ogni istruzione INSERT|4096|4096|  
|Connessioni per ogni client|Valore massimo delle connessioni configurate|Valore massimo delle connessioni configurate|  
|Dimensioni di database|524.272 terabytes|524.272 terabytes|  
|Database per ogni istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|32.767|32.767|  
|Filegroup per ogni database|32.767|32.767|  
|Filegroup per ogni database per dati ottimizzati per la memoria|Non supportato|1|  
|File per ogni database|32.767|32.767|  
|Dimensioni di file (dati)|16 terabyte|16 terabyte|  
|Dimensioni del file (log)|2 terabyte|2 terabyte|  
|File di dati per dati ottimizzati per la memoria per ogni database|Non supportato|4.096|  
|File differenziale per ogni file di dati per dati ottimizzati per la memoria|Non supportato|1|  
|Riferimenti alla tabella della chiave esterna per ogni tabella<br /><br /> Nota: Anche se una tabella può contenere un numero illimitato di vincoli FOREIGN KEY, il valore massimo consigliato è 253. A seconda della configurazione hardware che ospita [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], la specifica di altri vincoli FOREIGN KEY può risultare dispendiosa in termini di elaborazione da parte di Query Optimizer.|253|253|  
|Lunghezza di identificatore (in caratteri)|128|128|  
|Istanze per ogni computer|50 istanze in un server autonomo per tutte le edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta 25 istanze su un failover cluster quando si usa un disco cluster condiviso come opzione archiviata per l'installazione del cluster [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] condivisioni di file supporta 50 istanze in un failover cluster se si sceglie di SMB come opzione di archiviazione per l'installazione del cluster Per altre informazioni, vedere [Hardware and Software Requirements for Installing SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md).|50 istanze in un server autonomo.<br /><br /> 25 istanze su un cluster di failover durante l'utilizzo di un disco di cluster condiviso come opzione archiviata per l'installazione del cluster [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta 50 istanze su un cluster di failover se si scelgono condivisioni file SMB come opzione di archiviazione per l'installazione del cluster.|  
|Indici per ogni tabella ottimizzata per la memoria|Non supportato|8|  
|Lunghezza di una stringa contenente istruzioni SQL (dimensioni batch)<br /><br /> Nota: Dimensioni pacchetto di rete corrisponde alle dimensioni dei pacchetti del flusso TDS (Tabular Data Stream) usati per le comunicazioni tra applicazioni e [!INCLUDE[ssDE](../includes/ssde-md.md)]relazionale. La dimensione predefinita del pacchetto è 4 KB e viene controllata dall'opzione di configurazione delle dimensioni del pacchetto di rete.|65.536 * dimensioni del pacchetto di rete|65.536 * dimensioni del pacchetto di rete|  
|Blocchi per ogni connessione|Numero massimo di blocchi per ogni server|Numero massimo di blocchi per ogni server|  
|Blocchi per ogni istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]<br /><br /> Nota: Questo valore si riferisce all'allocazione di blocchi statici. I blocchi dinamici sono limitati solo dalla memoria.|Fino a 2.147.483.647|Limitato solo dalla memoria|  
|Livelli di nidificazione delle stored procedure<br /><br /> Nota: Se una stored procedure accede a più di 64 database o a più di 2 database in interfoliazione, verrà generato un errore.|32|32|  
|Sottoquery nidificate|32|32|  
|Livelli di nidificazione dei trigger|32|32|  
|Indici non cluster per tabella|999|999|  
|Numero di espressioni distinte nella clausola GROUP BY quando si verifica una delle operazioni seguenti: CUBE, ROLLUP, GROUPING SETS, WITH CUBE, WITH ROLLUP|32|32|  
|Numero di set di raggruppamento generati dagli operatori nella clausola GROUP BY|4.096|4.096|  
|Parametri per ogni stored procedure|2.100|2.100|  
|Parametri per ogni funzionalità definita dall'utente|2.100|2.100|  
|REFERENCES per ogni tabella|253|253|  
|Righe per ogni tabella|Limitato dall'archiviazione disponibile|Limitato dall'archiviazione disponibile|  
|Tabelle per ogni database<br /><br /> Nota: Gli oggetti di database possono essere tabelle, viste, stored procedure, funzioni definite dall'utente, trigger, regole, impostazioni predefinite e vincoli. La somma del numero di tutti gli oggetti in un database non può essere maggiore di 2.147.483.647.|Limitato dal numero di oggetti di un database|Limitato dal numero di oggetti di un database|  
|Partizioni per ogni tabella o indice partizionato|1.000<br /><br /> **\*\* Importanti \* \***  creazione di una tabella o indice con più di 1000 partizioni è possibile in un sistema a 32 bit, ma non è supportata.|15.000|  
|Statistiche relative a colonne non indicizzate|30.000|30.000|  
|Tabelle per ogni istruzione SELECT|Limitato solo dalle risorse disponibili|Limitato solo dalle risorse disponibili|  
|Trigger per ogni tabella<br /><br /> Nota: Gli oggetti di database possono essere tabelle, viste, stored procedure, funzioni definite dall'utente, trigger, regole, impostazioni predefinite e vincoli. La somma del numero di tutti gli oggetti in un database non può essere maggiore di 2.147.483.647.|Limitato dal numero di oggetti di un database|Limitato dal numero di oggetti di un database|  
|Colonne per ogni istruzione UPDATE (tabelle estese in larghezza)|4096|4096|  
|Connessioni utente|32.767|32.767|  
|Indici XML|249|249|  
  
##  <a name="Utility"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Oggetti Utilità  
 Nella tabella seguente vengono indicati le dimensioni e i numeri massimi dei diversi oggetti sottoposti a test in Utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Oggetto Utilità|Quantità/dimensioni massime [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bit)|Quantità/dimensioni massime [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bit)|  
|----------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Computer (computer fisici o macchine virtuali) per Utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|100|100|  
|Istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per ogni computer|5|5|  
|Numero complessivo di istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per Utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|200*|200*|  
|Database utente per ogni istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], incluse applicazioni livello dati|50|50|  
|Numero complessivo di database utente per Utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|1.000|1.000|  
|Filegroup per ogni database|1|1|  
|File di dati per filegroup|1|1|  
|File di log per ogni database|1|1|  
|Volumi per ogni computer|3|3|  
  
 * Il numero massimo di istanze gestite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supportati da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Utility possono variare in base alla configurazione hardware del server. Per informazioni introduttive, vedere [Attività e funzionalità di Utilità SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md). Il punto di controllo dell'utilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non è disponibile in tutte le edizione di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
##  <a name="DAC"></a> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Oggetti applicazione livello dati (DAC)  
 Nella tabella seguente vengono indicati le dimensioni e i numeri massimi dei diversi oggetti sottoposti a test nelle applicazioni livello dati (DAC) di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Oggetto applicazione livello dati|Quantità/dimensioni massime [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bit)|Quantità/dimensioni massime [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bit)|  
|------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Database per ogni applicazione livello dati|1|1|  
|Oggetti per ogni applicazione livello dati|Limitati dal numero di oggetti in un database o dalla memoria disponibile.|Limitati dal numero di oggetti in un database o dalla memoria disponibile.|  
  
 I tipi di oggetti inclusi nel limite sono utenti, tabelle, viste, stored procedure, funzioni definite dall'utente, tipi di dati definiti dall'utente, ruoli di database, schemi e tipi di tabella definiti dall'utente.  
  
##  <a name="Replication"></a> Oggetti di replica  
 Nella tabella seguente vengono indicati le dimensioni e i numeri massimi dei diversi oggetti definiti nella replica di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Oggetto replica|Dimensioni/numeri massimi per SQL Server (32 bit)|Dimensioni/numeri massimi per SQL Server (64 bit)|  
|--------------------------------------------------|---------------------------------------------------|---------------------------------------------------|  
|Articoli (pubblicazione di tipo merge)|256|256|  
|Articoli (pubblicazione snapshot o transazionale)|32.767|32.767|  
|Colonne in una tabella* (pubblicazione di tipo merge)|246|246|  
|Colonne in una tabella** (pubblicazione snapshot o transazionale di[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] )|1.000|1.000|  
|Colonne in una tabella** (pubblicazione snapshot o transazionale di Oracle)|995|995|  
|Byte per una colonna utilizzata in un filtro di riga (pubblicazione di tipo merge)|1.024|1.024|  
|Byte per una colonna utilizzata in un filtro di riga (pubblicazione snapshot o transazionale)|8.000|8.000|  
  
 *Se si usa il rilevamento a livello di riga per il rilevamento dei conflitti (impostazione predefinita), la tabella di base può includere fino a 1.024 colonne, che devono tuttavia essere filtrate dall'articolo in modo da pubblicare un massimo di 246 colonne. Se viene utilizzato il rilevamento a livello di colonna, nella tabella di base possono essere incluse al massimo 246 colonne.  
  
 **La tabella di base può includere il numero massimo di colonne consentito nel database di pubblicazione (1.024 per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), ma le colonne devono essere filtrate dall'articolo se superano il numero specificato per il tipo di pubblicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti hardware e Software per l'installazione di SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Parametri di controllo di Controllo configurazione sistema](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [Attività e funzionalità di Utilità SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
