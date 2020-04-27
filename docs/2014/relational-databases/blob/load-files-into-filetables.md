---
title: Caricare file in FileTable | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], migrating files
- FileTables [SQL Server], bulk loading
- FileTables [SQL Server], loading files
ms.assetid: dc842a10-0586-4b0f-9775-5ca0ecc761d9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43e5a9a6adcca7504aa90825ecd10e53e669c7e2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66010005"
---
# <a name="load-files-into-filetables"></a>Caricamento di file in FileTable
  Viene descritto come caricare o eseguire la migrazione dei file in tabelle FileTable.  
  
##  <a name="loading-or-migrating-files-into-a-filetable"></a><a name="BasicsLoadNew"></a> Caricamento o migrazione di file in tabelle FileTable  
 Il metodo scelto per il caricamento o la migrazione di file in una tabella FileTable dipende dalla posizione in cui sono attualmente archiviati i file.  
  
|Attuale posizione dei file|Opzioni per migrazione|  
|-------------------------------|---------------------------|  
|I file sono attualmente archiviati nel file system.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non dispone di conoscenza dei file.|Poiché una tabella FileTable viene visualizzata come cartella nel file system di Windows, è possibile caricare facilmente file in un nuova tabella FileTable tramite alcuni dei metodi disponibili per lo spostamento o la copia di file. Questi metodi includono Esplora risorse, opzioni della riga di comando come xcopy e robocopy e applicazioni o script personalizzati.<br /><br /> Non è possibile convertire una cartella esistente in tabella FileTable.|  
|I file sono attualmente archiviati nel file system.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include una tabella di metadati contenente puntatori ai file.|Il primo passaggio consiste nello spostare o copiare i file tramite uno dei metodi indicati in precedenza.<br /><br /> Il secondo passaggio consiste nell'aggiornare la tabella esistente di metadati in modo che punti alla nuova posizione dei file.<br /><br /> Per ulteriori informazioni, vedere [Esempio: Migrazione di file dal file system in una tabella FileTable](#HowToMigrateFiles) in questo argomento.|  
  
###  <a name="how-to-load-files-into-a-filetable"></a><a name="HowToLoadNew"></a> Procedura: Caricare file in una tabella FileTable  
 Tra i metodi che è possibile utilizzare per caricare file in una tabella FileTable sono inclusi i seguenti:  
  
-   Trascinare e rilasciare file dalle cartelle di origine alla nuova cartella FileTable in Esplora risorse.  
  
-   Utilizzare opzioni della riga di comando quali MOVE, COPY, XCOPY o ROBOCOPY dal prompt dei comandi o in un file batch o uno script.  
  
-   Scrivere un'applicazione personalizzata in C# o Visual Basic.NET che utilizzi metodi dello spazio dei nomi **System.IO** per spostare o copiare i file.  
  
###  <a name="example-migrating-files-from-the-file-system-into-a-filetable"></a><a name="HowToMigrateFiles"></a> Esempio: Migrazione di file dal file system in una tabella FileTable  
 In questo scenario i file vengono archiviati nel file system ed è disponibile una tabella di metadati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente puntatori ai file. Si desidera spostare i file in una tabella FileTable, quindi sostituire il percorso UNC originale per ogni file nei metadati con il percorso UNC della tabella FileTable. La funzione [GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql) consente di raggiungere tale obiettivo.  
  
 Per questo esempio, si supponga di disporre di una tabella di database `PhotoMetadata`esistente,, che contiene dati sulle fotografie. Questa tabella contiene una colonna `UNCPath` di tipo `varchar`(512) contenente il percorso UNC effettivo di un file con estensione jpg.  
  
 Per eseguire la migrazione dei file di immagine dal file system in una tabella FileTable, è necessario effettuare le operazioni seguenti:  
  
1.  Creare una nuova tabella FileTable che contenga i file. In questo esempio si usa il nome di tabella `dbo.PhotoTable` ma non viene illustrato il codice per creare la tabella.  
  
2.  Utilizzare xcopy o uno strumento simile per copiare i file JPG, con la relativa struttura di directory, nella directory radice della tabella FileTable.  
  
3.  Correggere i metadati nella tabella `PhotoMetadata` tramite codice simile al seguente:  
  
```sql  
--  Add a path locator column to the PhotoMetadata table.  
ALTER TABLE PhotoMetadata ADD pathlocator hierarchyid;  
  
-- Get the root path of the Photo directory on the File Server.  
DECLARE @UNCPathRoot varchar(100) = '\\RemoteShare\Photographs';  
  
-- Get the root path of the FileTable.  
DECLARE @FileTableRoot varchar(1000);  
SELECT @FileTableRoot = FileTableRootPath('dbo.PhotoTable');  
  
-- Update the PhotoMetadata table.  
  
-- Replace the File Server UNC path with the FileTable path.  
UPDATE PhotoMetadata  
    SET UNCPath = REPLACE(UNCPath, @UNCPathRoot, @FileTableRoot);  
  
-- Update the pathlocator column to contain the pathlocator IDs from the FileTable.  
UPDATE PhotoMetadata  
    SET pathlocator = GetPathLocator(UNCPath);  
```  
  
##  <a name="bulk-loading-files-into-a-filetable"></a><a name="BasicsBulkLoad"></a> Caricamento bulk di file in una tabella FileTable  
 Una tabella FileTable si comporta come una normale tabella per operazioni bulk, con le caratteristiche seguenti.  
  
 Una tabella FileTable include vincoli definiti dal sistema che garantiscono l'integrità dello spazio dei nomi di file/directory. È necessario verificare questi vincoli per i dati caricati in bulk nella tabella FileTable. Poiché alcune operazioni di inserimento bulk consentono di ignorare i vincoli di tabella, si applicano i requisiti seguenti.  
  
-   Le operazioni di caricamento bulk che impongono vincoli possono essere eseguite su una tabella FileTable esattamente come su qualsiasi altra tabella. Questa categoria include le operazioni seguenti:  
  
    -   bcp con clausola CHECK_CONSTRAINTS.  
  
    -   BULK INSERT con clausola CHECK_CONSTRAINTS.  
  
    -   INSERISCI IN... SELECT * FROM OPENROWSET (BULK...) senza clausola IGNORE_CONSTRAINTS.  
  
-   Le operazioni di caricamento bulk che non applicano vincoli hanno esito negativo a meno i vincoli definiti dal sistema della tabella FileTable non siano stati disabilitati. Questa categoria include le operazioni seguenti:  
  
    -   bcp senza clausola CHECK_CONSTRAINTS.  
  
    -   BULK INSERT senza clausola CHECK_CONSTRAINTS.  
  
    -   INSERISCI IN... SELECT * FROM OPENROWSET (BULK...) con IGNORE_CONSTRAINTS clausola.  
  
###  <a name="how-to-bulk-load-files-into-a-filetable"></a><a name="HowToBulkLoad"></a> Procedura: Caricamento bulk di file in una tabella FileTable  
 È possibile utilizzare diversi metodi per eseguire il caricamento bulk di file in una tabella FileTable:  
  
-   **bcp**  
  
    -   Eseguire una chiamata con la clausola **CHECK_CONSTRAINTS** .  
  
    -   Disabilitare lo spazio dei nomi FileTable ed eseguire una chiamata senza la clausola **CHECK_CONSTRAINTS** . Riabilitare quindi lo spazio dei nomi FileTable.  
  
-   **BULK INSERT**  
  
    -   Eseguire una chiamata con la clausola **CHECK_CONSTRAINTS** .  
  
    -   Disabilitare lo spazio dei nomi FileTable ed eseguire una chiamata senza la clausola **CHECK_CONSTRAINTS** . Riabilitare quindi lo spazio dei nomi FileTable.  
  
-   **INSERISCI IN... SELECT \* FROM OPENROWSET (bulk...)**  
  
    -   Eseguire una chiamata con la clausola **IGNORE_CONSTRAINTS** .  
  
    -   Disabilitare lo spazio dei nomi FileTable ed eseguire una chiamata senza la clausola **IGNORE_CONSTRAINTS** . Riabilitare quindi lo spazio dei nomi FileTable.  
  
 Per informazioni su come disabilitare i vincoli FileTable, vedere [Gestire le tabelle FileTable](manage-filetables.md).  
  
###  <a name="how-to-disable-filetable-constraints-for-bulk-loading"></a><a name="disabling"></a> Procedura: Disabilitare i vincoli FileTable per il caricamento bulk  
 Per eseguire il caricamento bulk di file in una tabella FileTable senza la necessità di applicare vincoli definiti dal sistema, è possibile disabilitare temporaneamente i vincoli. Per altre informazioni, vedere [Gestire le tabelle FileTable](manage-filetables.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Accedere a tabelle FileTable con Transact-SQL](access-filetables-with-transact-sql.md)   
 [Accedere alle tabelle FileTable con API di Input-Output dei file](access-filetables-with-file-input-output-apis.md)  
  
  
