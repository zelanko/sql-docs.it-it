---
title: Usare directory e percorsi in FileTable | Microsoft Docs
description: La funzionalità FileTable usa una struttura di directory per archiviare i file. Informazioni su come gestire gli elementi correlati a questa funzionalità ovvero directory, percorsi, restrizioni e semantica.
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], directories
ms.assetid: f1e45900-bea0-4f6f-924e-c11e1f98ab62
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4ab8501b5b0753143ce5bfe2b289211729c35821
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765465"
---
# <a name="work-with-directories-and-paths-in-filetables"></a>Utilizzare directory e percorsi in FileTable
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Descrive la struttura di directory nella quale vengono archiviati i file in FileTable.  
  
##  <a name="how-to-work-with-directories-and-paths-in-filetables"></a><a name="HowToDirectories"></a> Procedura: Utilizzare directory e percorsi in FileTable  
 Sono disponibili 3 funzioni che consentono di utilizzare le directory FileTable in [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
|Per ottenere questo risultato|Utilizzare questa funzione|  
|------------------------|-----------------------|  
|Ottenere il percorso UNC del livello radice di una specifica tabella FileTable o del database corrente.|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|  
|Ottenere un percorso UNC assoluto o relativo di un file o una directory in una tabella FileTable.|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|  
|Ottenere il valore dell'ID di posizione del percorso di una directory o di un file specificato in una tabella FileTable, indicandone il percorso.|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|  
  
##  <a name="how-to-use-relative-paths-for-portable-code"></a><a name="BestPracticeRelativePaths"></a> Procedura: Usare percorsi relativi per il codice portabile  
 Per mantenere il codice e le applicazioni indipendenti dal database e dal computer correnti, evitare di scrivere codice basato su percorsi di file assoluti. Ottenere invece il percorso completo di un file al runtime mediante l'uso combinato delle funzioni [FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md) e [GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md), come illustrato nell'esempio seguente. Per impostazione predefinita, la funzione **GetFileNamespacePath** restituisce il percorso relativo del file all'interno del percorso radice per il database.  
  
```sql  
USE database_name;  
DECLARE @root nvarchar(100);  
DECLARE @fullpath nvarchar(1000);  
  
SELECT @root = FileTableRootPath();  
SELECT @fullpath = @root + file_stream.GetFileNamespacePath()  
    FROM filetable_name  
    WHERE name = N'document_name';  
  
PRINT @fullpath;  
GO  
```  
  
##  <a name="important-restrictions"></a><a name="restrictions"></a> Restrizioni importanti  
  
###  <a name="nesting-level"></a><a name="nesting"></a> Livello di nidificazione  
  
> **IMPORTANTE** Non è possibile archiviare più di 15 livelli di sottodirectory nella directory FileTable. Quando si archiviano 15 livelli di sottodirectory, il livello più basso non può contenere file, poiché essi rappresenterebbero un ulteriore livello.  
  
###  <a name="length-of-full-path-name"></a><a name="fqnlength"></a> Lunghezza del nome e percorso completo  
  
> **IMPORTANTE** Il file system NTFS supporta nomi di percorso la cui lunghezza supera il limite di 260 caratteri della shell di Windows e della maggior parte delle API Windows. Pertanto, utilizzando Transact-SQL, è possibile creare file nella gerarchia dei file di una tabella FileTable che non è possibile visualizzare o aprire con Esplora risorse o con molte altre applicazioni Windows, perché il nome e percorso completo superano i 260 caratteri. Tuttavia, è possibile continuare ad accedere a questi file tramite Transact-SQL.  
  
##  <a name="the-full-path-to-an-item-stored-in-a-filetable"></a><a name="fullpath"></a> Percorso completo di un elemento archiviato in una tabella FileTable  
 Il percorso completo di un file o di una directory in una tabella FileTable inizia con gli elementi seguenti:  
  
1.  Condivisione abilitata per l'accesso di I/O ai file FILESTREAM a livello dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  **DIRECTORY_NAME** specificato a livello di database.  
  
3.  **FILETABLE_DIRECTORY** specificato a livello di FileTable.  

 La gerarchia risultante risulta analoga alla seguente:  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\`  
  
 Questa gerarchia di directory costituisce la radice di uno spazio dei nomi dei file di FileTable. In questa gerarchia di directory, i dati FILESTREAM per la tabella FileTable vengono archiviati come file e come sottodirectory che possono a loro volta contenere file e sottodirectory.  
  
 È importante ricordare che la gerarchia di directory creata nella condivisione FILESTREAM a livello di istanza è una gerarchia di directory virtuale. Questa gerarchia viene archiviata nel database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non è rappresentata fisicamente nel file system NTFS. Tutte le operazioni che comportano l'accesso a file e directory nella condivisione FILESTREAM e nelle tabelle FileTable in essa contenute sono intercettate e gestite da un componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incorporato nel file system.  
  
##  <a name="the-semantics-of-the-root-directories-at-the-instance-database-and-filetable-levels"></a><a name="roots"></a> Semantica delle directory radice a livello di istanza, database e tabella FileTable  
 Questa gerarchia di directory osserva la semantica seguente:  
  
-   La condivisione FILESTREAM del livello di istanza viene configurata da un amministratore e archiviata come proprietà del server. È possibile rinominare la condivisione mediante Gestione configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'operazione di ridenominazione non viene applicata finché il server non viene riavviato.  
  
-   Per impostazione predefinita, l'elemento **DIRECTORY_NAME** a livello di database è null quando si crea un nuovo database. Un amministratore può impostare o modificare il nome mediante l'istruzione **ALTER DATABASE** . Il nome deve essere univoco (in un confronto senza distinzione fra maiuscole e minuscole) nell'istanza in questione.  
  
-   In genere, il nome **FILETABLE_DIRECTORY** viene specificato con l'istruzione **CREATE TABLE** al momento di creare una tabella FileTable. È possibile modificare questo nome mediante il comando **ALTER TABLE** .  
  
-   Non è possibile rinominare queste directory radice tramite operazioni di I/O su file.  
  
-   Non è possibile aprire queste directory radice con handle di file esclusivi.  
  
##  <a name="the-is_directory-column-in-the-filetable-schema"></a><a name="is_directory"></a> Colonna is_directory nello schema della tabella FileTable  
 La tabella seguente descrive l'interazione tra la colonna **is_directory** e la colonna **file_stream** contenente i dati FILESTREAM in una tabella FileTable.  
  
||||  
|-|-|-|  
|*is_directory* **value**|*file_stream* **value**|**Comportamento**|  
|FALSE|NULL|Si tratta di una combinazione non valida che sarà intercettata da un vincolo definito dal sistema.|  
|FALSE|\<value>|L'elemento rappresenta un file.|  
|TRUE|NULL|L'elemento rappresenta una directory.|  
|TRUE|\<value>|Si tratta di una combinazione non valida che sarà intercettata da un vincolo definito dal sistema.|  
  
##  <a name="using-virtual-network-names-vnns-with-alwayson-availability-groups"></a><a name="alwayson"></a> Utilizzo di nomi di rete virtuale con i gruppi di disponibilità AlwaysOn  
 Quando il database che contiene dati FILESTREAM o FileTable appartiene a un gruppo di disponibilità AlwaysOn:  
  
-   Le funzioni FILESTREAM e FileTable accettano o restituiscono nomi di rete virtuale anziché nomi computer. Per altre informazioni su queste funzioni, vedere [Funzioni FileStream e FileTable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filestream-and-filetable-functions-transact-sql.md).  
  
-   Ogni accesso a dati FILESTREAM o FileTable tramite le API del file system deve utilizzare VNN anziché nomi computer. Per altre informazioni, vedere [FILESTREAM e FileTable con i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitazione dei prerequisiti per la tabella FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)   
 [Creare, modificare e rilasciare FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [Accesso a tabelle FileTable tramite Transact-SQL](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [Accedere alle tabelle FileTable con API di input/output dei file](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
  
  
