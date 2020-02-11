---
title: Tabelle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server]
- table components [SQL Server]
ms.assetid: 82d7819c-b801-4309-a849-baa63083e83f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7a456d68283d81cf7eb4f879d76f086484c5e052
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211784"
---
# <a name="tables"></a>Tabelle
  Le tabelle sono oggetti di database che contengono tutti i dati presenti in un database. Nelle tabelle, i dati sono organizzati in modo logico in righe e colonne in un formato simile a quello di un foglio di calcolo. Ogni riga rappresenta un record univoco e ogni colonna rappresenta un campo all'interno del record. Ad esempio, una tabella che include i dati dei dipendenti di un'azienda può contenere una riga per ogni dipendente e colonne che rappresentano i dettagli dei dipendenti quali l'ID, il nome, l'indirizzo, la posizione e il numero di telefono dell'abitazione.  
  
-   Il numero di tabelle presenti in un database è limitato solo dal numero di oggetti disponibili in un database (2,147,483,647). Una tabella standard definita dall'utente può avere fino a 1.024 colonne. Il numero di righe nella tabella è limitato solo dalla capacità di archiviazione del server.  
  
-   È possibile assegnare proprietà alla tabella e a ogni colonna nella tabella per controllare i dati consentiti e le altre proprietà. Ad esempio, è possibile creare vincoli in una colonna per impedire valori null o fornire un valore predefinito se non è specificato un valore oppure è possibile assegnare un vincolo principale sulla tabella che applica l'univocità o definisce una relazione tra tabelle.  
  
-   I dati nella tabella possono essere compressi per riga o per pagina. La compressione dei dati può consentire l'archiviazione di più righe su una pagina. Per altre informazioni, vedere [Data Compression](../../relational-databases/data-compression/data-compression.md).  
  
## <a name="types-of-tables"></a>Tipi di tabelle  
 Oltre al ruolo standard delle tabelle di base definite dall'utente, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono disponibili i tipi di tabelle seguenti per scopi specifici in un database:  
  
 Tabelle partizionate  
 Nelle tabelle partizionate, i dati vengono suddivisi orizzontalmente in unità che possono essere distribuite in più filegroup di un database. Il partizionamento semplifica la gestione di tabelle o indici di grandi dimensioni in quanto consente di gestire o accedere a subset di dati in modo rapido ed efficace mantenendo l'integrità della raccolta. Per impostazione predefinita, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] supporta fino a 15.000 partizioni. Per ulteriori informazioni, vedere [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 Tabelle temporanee  
 Le tabelle temporanee vengono archiviate in `tempdb`. Esistono due tipi di tabelle temporanee, ovvero le tabelle locali e le tabelle globali. I due tipi differiscono per i nomi, la visibilità e la disponibilità. Le tabelle temporanee locali contengono un solo simbolo di cancelletto (#) come primo carattere del nome, sono visibili solo durante la connessione utente corrente e vengono eliminate quando l'utente chiude la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Le tabelle temporanee globali contengono due simboli di cancelletto (##) come primi caratteri del nome, una volta create sono visibili per tutti gli utenti e vengono eliminate quando tutti gli utenti che fanno riferimento alla tabella chiudono la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Tabelle di sistema  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Archivia i dati che definiscono la configurazione del server e di tutte le relative tabelle in un set di tabelle speciale noto come tabelle di sistema. Gli utenti non possono eseguire una query direttamente o aggiornare le tabelle di sistema. Le informazioni delle tabelle di sistema vengono rese disponibili tramite le viste di sistema. Per altre informazioni, vedere [Viste di sistema &#40;Transact-SQL&#41;](/sql/t-sql/language-reference).  
  
 Tabelle estese in larghezza  
 Le tabelle estese in larghezza usano le [colonne di tipo sparse](use-sparse-columns.md) per aumentare a 30.000 il numero totale di colonne che una tabella può contenere. Le colonne di tipo sparse sono colonne comuni che dispongono di archiviazione ottimizzata per i valori Null. Tali colonne consentono di ridurre i requisiti di spazio per i valori Null aumentando tuttavia l'overhead per il recupero dei valori non Null. Una colonna estesa ha definito un [set di colonne](use-column-sets.md), ovvero una rappresentazione XML non tipizzata che combina tutte le colonne di tipo sparse di una tabella in un output strutturato. Anche il numero degli indici e delle statistiche viene portato rispettivamente a 1.000 e 30.000. Le dimensioni di una riga di tabella estesa in larghezza non possono superare 8.019 byte. Pertanto, la maggior parte dei dati di qualsiasi riga deve essere NULL. Il numero massimo di colonne di tipo nonsparse più le colonne calcolate di una tabella estesa in larghezza rimane 1.024.  
  
 Le tabelle estese in larghezza hanno le seguenti implicazioni sulle prestazioni.  
  
-   Le tabelle estese in larghezza possono aumentare i costi di gestione degli indici nella tabella. È consigliabile limitare il numero di indici di una tabella estesa in larghezza agli indici richiesti dalla logica di business. All'aumento del numero di indici corrisponde infatti un aumento dei requisiti di memoria e dei tempi di compilazione DML. Gli indici non cluster devono essere indici filtrati applicati a subset di dati. Per altre informazioni, vedere [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
-   Tramite applicazioni è possibile aggiungere e rimuovere in modo dinamico le colonne dalle tabelle estese in larghezza. Quando si aggiungono o rimuovono colonne, i piani di query compilati perdono validità. È pertanto consigliabile progettare un'applicazione in base al carico di lavoro previsto in modo che le modifiche allo schema siano minime.  
  
-   L'aggiunta e la rimozione di dati da una tabella estesa in larghezza possono incidere negativamente sulle prestazioni. È necessario progettare le applicazioni per il carico di lavoro previsto in modo che le modifiche ai dati della tabella siano minime.  
  
-   Limitare l'esecuzione di istruzioni DML in una tabella estesa in larghezza che comportino l'aggiornamento di più righe di una chiave di clustering. La compilazione e l'esecuzione di queste istruzioni possono richiedere una notevole quantità di memoria.  
  
-   Il passaggio tra partizioni nelle tabelle estese in larghezza può essere lento e richiedere grandi quantità di memoria di elaborazione. Le prestazioni e i requisiti di memoria sono proporzionali al numero totale di colonne sia nella partizione di origine sia in quella di destinazione.  
  
-   I cursori di aggiornamento di colonne specifiche di una tabella estesa in larghezza dovrebbero elencare le colonne in modo esplicito per la clausola FOR UPDATE. In questo modo, è possibile ottimizzare le prestazioni quando si utilizzano i cursori.  
  
## <a name="common-table-tasks"></a>Attività comuni della tabella  
 Nella tabella riportata di seguito vengono forniti i collegamenti a attività comuni associate alla creazione o alla modifica di una tabella.  
  
|Attività tabella|Argomento|  
|-----------------|-----------|  
|Viene illustrato come creare una tabella.|[Creare tabelle &#40;motore di database&#41;](create-tables-database-engine.md)|  
|Viene illustrato come eliminare una tabella.|[Elimina tabelle &#40;motore di database&#41;](delete-tables-database-engine.md)|  
|Viene illustrato come creare una nuova tabella che contiene alcune o tutte le colonne in una tabella esistente.|[Duplicare le tabelle](duplicate-tables.md)|  
|Viene illustrato come ridenominare una tabella.|[Rinominare le tabelle &#40;motore di database&#41;](rename-tables-database-engine.md)|  
|Viene illustrata la procedura per visualizzare le proprietà della tabella.|[Visualizzare la definizione di una tabella](view-the-table-definition.md)|  
|Viene illustrato come determinare se altri oggetti quali una vista o una stored procedure dipende da una tabella.|[Visualizzare le dipendenze di una tabella](view-the-dependencies-of-a-table.md)|  
  
 Nella tabella riportata di seguito vengono forniti i collegamenti a attività comuni associate alla creazione o alla modifica di colonne in una tabella.  
  
|Attività colonne|Argomento|  
|------------------|-----------|  
|Viene illustrato come aggiungere colonne a una tabella esistente.|[Aggiungere colonne a una tabella &#40;motore di database&#41;](add-columns-to-a-table-database-engine.md)|  
|Viene illustrato come eliminare colonne da una tabella.|[Eliminare le colonne da una tabella](delete-columns-from-a-table.md)|  
|Viene illustrato come modificare il nome di una colonna.|[Rinominare le colonne &#40;motore di database&#41;](rename-columns-database-engine.md)|  
|Viene illustrato come copiare colonne da una tabella a un'altra copiando solo la definizione di colonna oppure la definizione e i dati.|[Copiare colonne da una tabella a un'altra &#40;motore di database&#41;](copy-columns-from-one-table-to-another-database-engine.md)|  
|Viene illustrato come modificare una definizione di colonna, modificando il tipo di dati o altre proprietà.|[Modificare le colonne &#40;motore di database&#41;](modify-columns-database-engine.md)|  
|Viene illustrato come modificare l'ordine di visualizzazione delle colonne.|[Modificare l'ordine delle colonne in una tabella](change-column-order-in-a-table.md)|  
|Viene illustrato come creare una colonna calcolata in una tabella.|[Specificare le colonne calcolate in una tabella](specify-computed-columns-in-a-table.md)|  
|Viene illustrato come specificare un valore predefinito per una colonna. Questo valore viene utilizzato nel caso non venga fornito alcun altro valore.|[Specificare i valori predefiniti per le colonne](specify-default-values-for-columns.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Vincoli di chiave primaria ed esterna](primary-and-foreign-key-constraints.md)   
 [Vincoli UNIQUE e CHECK](unique-constraints-and-check-constraints.md)  
  
  
