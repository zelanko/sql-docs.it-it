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
ms.openlocfilehash: 59b45d3ab221e02b89abf328eac5f189f0f84728
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85044594"
---
# <a name="maximum-capacity-specifications-for-sql-server"></a>Specifiche di capacità massima per SQL Server
  Nelle tabelle seguenti vengono indicati le dimensioni e i numeri massimi dei diversi oggetti definiti nei componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per passare alla tabella per una tecnologia [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , fare clic sul relativo collegamento:  
  
 [Oggetti Motore di database di SQL Server](#Engine)  
  
 [Oggetti di Utilità SQL Server](#Utility)  
  
 [Oggetti applicazione livello dati di SQL Server](#DAC)  
  
 [Oggetti di replica di SQL Server](#Replication)  
  
##  <a name="ssde-objects"></a><a name="Engine"></a>[!INCLUDE[ssDE](../includes/ssde-md.md)]Oggetti di  
 Nella tabella seguente vengono indicati le dimensioni e i numeri massimi dei diversi oggetti definiti nei database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o a cui si fa riferimento nelle istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
|Oggetto [!INCLUDE[ssDE](../includes/ssde-md.md)] di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Dimensioni/numeri massimi [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bit)|Quantità/dimensioni massime [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bit)|  
|---------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Dimensioni dei batch<br /><br /> Nota: le dimensioni del pacchetto di rete corrispondono alle dimensioni dei pacchetti TDS (Tabular Data Stream) usati per le comunicazioni tra applicazioni e relazionali [!INCLUDE[ssDE](../includes/ssde-md.md)] . La dimensione predefinita del pacchetto è 4 KB e viene controllata dall'opzione di configurazione delle dimensioni del pacchetto di rete.|65.536 * dimensioni del pacchetto di rete|65.536 * dimensioni del pacchetto di rete|  
|Byte per ogni colonna di stringhe brevi|8\.000|8\.000|  
|Byte per ogni clausola GROUP BY, ORDER BY|8\.060|8\.060|  
|Byte per ogni chiave di indice<br /><br /> Nota: il numero massimo di byte in una chiave di indice non può essere maggiore di 900 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . È possibile definire una chiave utilizzando colonne di lunghezza variabile le cui dimensioni massime sono maggiori di 900, a condizione che non vengano inserite nelle colonne righe con più di 900 byte di dati. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è possibile includere in un indice non cluster colonne non chiave per evitare di raggiungere la dimensione massima di 900 byte consentita per le chiavi di indice.|900|900|  
|Byte per ogni chiave esterna|900|900|  
|Byte per ogni chiave primaria|900|900|  
|Byte per ogni riga<br /><br /> Nota:<br />        [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta l'archiviazione dei dati di overflow della riga che consente di spostare le colonne di lunghezza variabile all'esterno delle righe. Solo una radice di 24 byte viene archiviata nel record principale per le colonne di lunghezza variabile spostate all'esterno di righe. Di conseguenza, il limite delle righe effettivo è maggiore di quello delle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere l'argomento "Dati di overflow della riga che superano 8 KB" nella documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|8\.060|8\.060|  
|Byte per ogni riga nelle tabelle ottimizzate per la memoria<br /><br /> Nota:<br />        OLTP in memoria di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non supporta l'archiviazione dei dati di overflow della riga. Le colonne a lunghezza variabile non vengono spostate all'esterno delle righe. In questo modo viene limitata la larghezza massima delle colonne a lunghezza variabile che è possibile specificare in una tabella ottimizzata per la memoria alle dimensioni massime di riga. Per altre informazioni, vedere [Dimensioni di tabelle e righe per le tabelle con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md).|Non supportate|8\.060|  
|Byte nel testo di origine di una stored procedure|Minore delle dimensioni batch o 250 MB|Minore delle dimensioni batch o 250 MB|  
|Byte per ogni colonna `varchar(max)`, `varbinary(max)`, `xml`, `text` o `image`|2^31-1|2^31-1|  
|Caratteri per ogni colonna `ntext` o `nvarchar(max)`|2^30-1|2^30-1|  
|Indici cluster per tabella|1|1|  
|Colonne in GROUP BY, ORDER BY|Limitato solo dal numero di byte|Limitato solo dal numero di byte|  
|Colonne o espressioni in un'istruzione GROUP BY WITH CUBE o WITH ROLLUP|10|10|  
|Colonne per ogni chiave di indice<br /><br /> Nota: se la tabella contiene uno o più indici XML, la chiave di clustering della tabella utente è limitata a 15 colonne perché la colonna XML viene aggiunta alla chiave di clustering dell'indice XML primario. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]è possibile includere in un indice non cluster colonne non chiave per evitare di raggiungere il limite massimo di 16 colonne chiave. Per altre informazioni, vedere [Creare indici con colonne incluse](../relational-databases/indexes/create-indexes-with-included-columns.md).|16|16|  
|Colonne per ogni chiave esterna|16|16|  
|Colonne per ogni chiave primaria|16|16|  
|Colonne per ogni tabella non estesa in larghezza|1\.024|1\.024|  
|Colonne per ogni tabella estesa in larghezza|30.000|30.000|  
|Colonne per ogni istruzione SELECT|4\.096|4\.096|  
|Colonne per ogni istruzione INSERT|4096|4096|  
|Connessioni per ogni client|Valore massimo delle connessioni configurate|Valore massimo delle connessioni configurate|  
|Dimensioni del database|524.272 terabytes|524.272 terabytes|  
|Database per ogni istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|32.767|32.767|  
|Filegroup per ogni database|32.767|32.767|  
|Filegroup per ogni database per dati ottimizzati per la memoria|Non supportate|1|  
|File per ogni database|32.767|32.767|  
|Dimensioni di file (dati)|16 terabyte|16 terabyte|  
|Dimensioni del file (log)|2 terabyte|2 terabyte|  
|File di dati per dati ottimizzati per la memoria per ogni database|Non supportate|4.096|  
|File differenziale per ogni file di dati per dati ottimizzati per la memoria|Non supportate|1|  
|Riferimenti alla tabella della chiave esterna per ogni tabella<br /><br /> Nota: anche se una tabella può contenere un numero illimitato di vincoli di chiave esterna, il valore massimo consigliato è 253. A seconda della configurazione hardware che ospita [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], la specifica di altri vincoli FOREIGN KEY può risultare dispendiosa in termini di elaborazione da parte di Query Optimizer.|253|253|  
|Lunghezza di identificatore (in caratteri)|128|128|  
|Istanze per ogni computer|50 istanze in un server autonomo per tutte le edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]<br /><br /> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]supporta 25 istanze in un cluster di failover quando si utilizza un disco del cluster condiviso come opzione archiviata per l'installazione del cluster [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta le istanze 50 in un cluster di failover se si scelgono condivisioni file SMB come opzione di archiviazione per l'installazione del cluster per ulteriori informazioni, vedere [requisiti hardware e software per l'installazione di SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md).|50 istanze in un server autonomo.<br /><br /> 25 istanze su un cluster di failover durante l'utilizzo di un disco di cluster condiviso come opzione archiviata per l'installazione del cluster [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta 50 istanze su un cluster di failover se si scelgono condivisioni file SMB come opzione di archiviazione per l'installazione del cluster.|  
|Indici per ogni tabella ottimizzata per la memoria|Non supportate|8|  
|Lunghezza di una stringa contenente istruzioni SQL (dimensioni batch)<br /><br /> Nota: le dimensioni del pacchetto di rete corrispondono alle dimensioni dei pacchetti TDS (Tabular Data Stream) usati per le comunicazioni tra applicazioni e relazionali [!INCLUDE[ssDE](../includes/ssde-md.md)] . La dimensione predefinita del pacchetto è 4 KB e viene controllata dall'opzione di configurazione delle dimensioni del pacchetto di rete.|65.536 * dimensioni del pacchetto di rete|65.536 * dimensioni del pacchetto di rete|  
|Blocchi per ogni connessione|Numero massimo di blocchi per ogni server|Numero massimo di blocchi per ogni server|  
|Blocchi per ogni istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]<br /><br /> Nota: questo valore è per l'allocazione di blocchi statici. I blocchi dinamici sono limitati solo dalla memoria.|Fino a 2.147.483.647|Limitato solo dalla memoria|  
|Livelli di nidificazione delle stored procedure<br /><br /> Nota: se un stored procedure accede a più di 64 database o a più di 2 database in interfoliazione, verrà visualizzato un errore.|32|32|  
|Sottoquery nidificate|32|32|  
|Livelli di nidificazione dei trigger|32|32|  
|Indici non cluster per tabella|999|999|  
|Numero di espressioni distinte nella clausola GROUP BY quando è presente una delle seguenti opzioni: CUBE, ROLLUP, GROUPING SETS, WITH CUBE o WITH ROLLUP|32|32|  
|Numero di set di raggruppamento generati dagli operatori nella clausola GROUP BY|4\.096|4\.096|  
|Parametri per ogni stored procedure|2\.100|2\.100|  
|Parametri per ogni funzionalità definita dall'utente|2\.100|2\.100|  
|REFERENCES per ogni tabella|253|253|  
|Righe per ogni tabella|Limitato dall'archiviazione disponibile|Limitato dall'archiviazione disponibile|  
|Tabelle per ogni database<br /><br /> Nota: gli oggetti di database includono oggetti quali tabelle, viste, stored procedure, funzioni definite dall'utente, trigger, regole, impostazioni predefinite e vincoli. La somma del numero di tutti gli oggetti in un database non può essere maggiore di 2.147.483.647.|Limitato dal numero di oggetti di un database|Limitato dal numero di oggetti di un database|  
|Partizioni per ogni tabella o indice partizionato|1\.000<br /><br /> Importante la creazione di una tabella o di un indice con più di 1.000 partizioni è possibile in un sistema a 32 bit, ma non è supportato. ** \* \* \* \* **|15.000|  
|Statistiche relative a colonne non indicizzate|30.000|30.000|  
|Tabelle per ogni istruzione SELECT|Limitato solo dalle risorse disponibili|Limitato solo dalle risorse disponibili|  
|Trigger per ogni tabella<br /><br /> Nota: gli oggetti di database includono oggetti quali tabelle, viste, stored procedure, funzioni definite dall'utente, trigger, regole, impostazioni predefinite e vincoli. La somma del numero di tutti gli oggetti in un database non può essere maggiore di 2.147.483.647.|Limitato dal numero di oggetti di un database|Limitato dal numero di oggetti di un database|  
|Colonne per ogni istruzione UPDATE (tabelle estese in larghezza)|4096|4096|  
|Connessioni utente|32.767|32.767|  
|Indici XML|249|249|  
  
##  <a name="ssnoversion-utility-objects"></a><a name="Utility"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Oggetti utilità  
 Nella tabella seguente vengono indicati le dimensioni e i numeri massimi dei diversi oggetti sottoposti a test in Utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Oggetto Utilità|Dimensioni/numeri massimi [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bit)|Quantità/dimensioni massime [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bit)|  
|----------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Computer (computer fisici o macchine virtuali) per Utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|100|100|  
|Istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per ogni computer|5|5|  
|Numero complessivo di istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per Utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|200*|200*|  
|Database utente per ogni istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], incluse applicazioni livello dati|50|50|  
|Numero complessivo di database utente per Utilità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|1\.000|1\.000|  
|Filegroup per ogni database|1|1|  
|File di dati per filegroup|1|1|  
|File di log per ogni database|1|1|  
|Volumi per ogni computer|3|3|  
  
 * Il numero massimo di istanze gestite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supportate da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilità può variare in base alla configurazione hardware del server. Per informazioni introduttive, vedere [Attività e funzionalità di Utilità SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md). Il punto di controllo dell'utilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non è disponibile in tutte le edizione di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
##  <a name="ssnoversion-data-tier-application-objects"></a><a name="DAC"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Oggetti applicazione livello dati  
 Nella tabella seguente vengono indicati le dimensioni e i numeri massimi dei diversi oggetti sottoposti a test nelle applicazioni livello dati (DAC) di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Oggetto applicazione livello dati|Dimensioni/numeri massimi [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32 bit)|Quantità/dimensioni massime [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64 bit)|  
|------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|  
|Database per ogni applicazione livello dati|1|1|  
|Oggetti per ogni applicazione livello dati|Limitati dal numero di oggetti in un database o dalla memoria disponibile.|Limitati dal numero di oggetti in un database o dalla memoria disponibile.|  
  
 I tipi di oggetti inclusi nel limite sono utenti, tabelle, viste, stored procedure, funzioni definite dall'utente, tipi di dati definiti dall'utente, ruoli di database, schemi e tipi di tabella definiti dall'utente.  
  
##  <a name="replication-objects"></a><a name="Replication"></a>Oggetti di replica  
 Nella tabella seguente vengono indicati le dimensioni e i numeri massimi dei diversi oggetti definiti nella replica di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Oggetto replica|Dimensioni/numeri massimi per SQL Server (32 bit)|Dimensioni/numeri massimi per SQL Server (64 bit)|  
|--------------------------------------------------|---------------------------------------------------|---------------------------------------------------|  
|Articoli (pubblicazione di tipo merge)|256|256|  
|Articoli (pubblicazione snapshot o transazionale)|32.767|32.767|  
|Colonne in una tabella* (pubblicazione di tipo merge)|246|246|  
|Colonne in una tabella** (pubblicazione snapshot o transazionale di[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] )|1\.000|1\.000|  
|Colonne in una tabella** (pubblicazione snapshot o transazionale di Oracle)|995|995|  
|Byte per una colonna utilizzata in un filtro di riga (pubblicazione di tipo merge)|1\.024|1\.024|  
|Byte per una colonna utilizzata in un filtro di riga (pubblicazione snapshot o transazionale)|8\.000|8\.000|  
  
 *Se si usa il rilevamento a livello di riga per il rilevamento dei conflitti (impostazione predefinita), la tabella di base può includere fino a 1.024 colonne, che devono tuttavia essere filtrate dall'articolo in modo da pubblicare un massimo di 246 colonne. Se viene utilizzato il rilevamento a livello di colonna, nella tabella di base possono essere incluse al massimo 246 colonne.  
  
 **La tabella di base può includere il numero massimo di colonne consentito nel database di pubblicazione (1.024 per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), ma le colonne devono essere filtrate dall'articolo se superano il numero specificato per il tipo di pubblicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti hardware e software per l'installazione di SQL Server 2014](install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Parametri di controllo per controllo configurazione sistema](../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [Funzionalità e attività di Utilità SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
