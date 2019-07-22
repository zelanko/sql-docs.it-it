---
title: Caricare file in FileTable | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 9af9e8f2a1e54b4fbcbc935a3256d6cf3b100178
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125118"
---
# <a name="load-files-into-filetables"></a>Caricamento di file in FileTable
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Viene descritto come caricare o eseguire la migrazione dei file in tabelle FileTable.  
  
##  <a name="BasicsLoadNew"></a> Caricamento o migrazione di file in tabelle FileTable  
 Il metodo scelto per il caricamento o la migrazione di file in una tabella FileTable dipende dalla posizione in cui sono attualmente archiviati i file.  
  
|Attuale posizione dei file|Opzioni per migrazione|  
|-------------------------------|---------------------------|  
|I file sono attualmente archiviati nel file system.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non dispone di conoscenza dei file.|Poiché una tabella FileTable viene visualizzata come cartella nel file system di Windows, è possibile caricare facilmente file in un nuova tabella FileTable tramite alcuni dei metodi disponibili per lo spostamento o la copia di file. Questi metodi includono Esplora risorse, opzioni della riga di comando, ad esempio xcopy e robocopy, nonché applicazioni o script personalizzati.<br /><br /> Non è possibile convertire una cartella esistente in tabella FileTable.|  
|I file sono attualmente archiviati nel file system.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] include una tabella di metadati contenente puntatori ai file.|Il primo passaggio consiste nello spostare o copiare i file tramite uno dei metodi indicati in precedenza.<br /><br /> Il secondo passaggio consiste nell'aggiornare la tabella esistente di metadati in modo che punti alla nuova posizione dei file.<br /><br /> Per altre informazioni, vedere [Esempio: Migrazione di file dal file system in una tabella FileTable](#HowToMigrateFiles) in questo articolo.|  
  
###  <a name="HowToLoadNew"></a> Procedura: Caricare file in una tabella FileTable  
Per caricare i file in una tabella FileTable è possibile usare i metodi seguenti:  
  
-   Trascinare e rilasciare file dalle cartelle di origine alla nuova cartella FileTable in Esplora risorse.  
  
-   Usare opzioni della riga di comando quali MOVE, COPY, XCOPY o ROBOCOPY dal prompt dei comandi o in un file o script batch.  
  
-   Scrivere un'applicazione personalizzata per spostare o copiare i file in C# o Visual Basic.NET. Chiamare metodi dallo spazio dei nomi **System.IO**.  
  
###  <a name="HowToMigrateFiles"></a> Esempio: Migrazione di file dal file system in una tabella FileTable  
 In questo scenario i file vengono archiviati nel file system ed è disponibile una tabella di metadati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente puntatori ai file. Si desidera spostare i file in una tabella FileTable, quindi sostituire il percorso UNC originale per ogni file nei metadati con il percorso UNC della tabella FileTable. La funzione [GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md) consente di raggiungere tale obiettivo.  
  
 Per questo esempio, si supponga la disponibilità di una tabella di database esistente, denominata **PhotoMetadata**, che contiene dati su fotografie. Questa tabella include una colonna **UNCPath** di tipo **varchar**(512) contenente il percorso UNC effettivo di un file con estensione jpg.  
  
 Per eseguire la migrazione dei file di immagine dal file system in una tabella FileTable, seguire questa procedura:  
  
1.  Creare una nuova tabella FileTable che contenga i file. In questo esempio si usa il nome di tabella **dbo.PhotoTable**ma non viene illustrato il codice per creare la tabella.  
  
2.  Utilizzare xcopy o uno strumento simile per copiare i file JPG, con la relativa struttura di directory, nella directory radice della tabella FileTable.  
  
3.  Correggere i metadati nella tabella **PhotoMetadata** usando codice simile all'esempio seguente:  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

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
  
##  <a name="BasicsBulkLoad"></a> Caricamento bulk di file in una tabella FileTable  
 Una tabella FileTable si comporta come una normale tabella per operazioni bulk, con le caratteristiche seguenti:  
  
 Una tabella FileTable include vincoli definiti dal sistema che garantiscono l'integrità dello spazio dei nomi di file e directory. È necessario verificare questi vincoli per i dati caricati in bulk nella tabella FileTable. Poiché alcune operazioni di inserimento bulk consentono di ignorare i vincoli di tabella, si applicano i requisiti seguenti.  
  
-   Le operazioni di caricamento bulk che impongono vincoli possono essere eseguite su una tabella FileTable esattamente come su qualsiasi altra tabella. Questa categoria include le operazioni seguenti:  
  
    -   bcp con clausola CHECK_CONSTRAINTS.  
  
    -   BULK INSERT con clausola CHECK_CONSTRAINTS.  
  
    -   INSERT INTO ... SELECT * FROM OPENROWSET(BULK ...) senza la clausola IGNORE_CONSTRAINTS.  
  
-   Le operazioni di caricamento bulk che non applicano vincoli hanno esito negativo a meno i vincoli definiti dal sistema della tabella FileTable non siano stati disabilitati. Questa categoria include le operazioni seguenti:  
  
    -   bcp senza clausola CHECK_CONSTRAINTS.  
  
    -   BULK INSERT senza clausola CHECK_CONSTRAINTS.  
  
    -   INSERT INTO ... SELECT * FROM OPENROWSET(BULK ...) con la clausola IGNORE_CONSTRAINTS.  
  
###  <a name="HowToBulkLoad"></a> Procedura: Eseguire il caricamento bulk di file in una tabella FileTable  
 È possibile utilizzare diversi metodi per eseguire il caricamento bulk di file in una tabella FileTable:  
  
-   **bcp**  
  
    -   Eseguire una chiamata con la clausola **CHECK_CONSTRAINTS** .  
  
    -   Disabilitare lo spazio dei nomi FileTable ed eseguire una chiamata senza la clausola **CHECK_CONSTRAINTS** . Riabilitare quindi lo spazio dei nomi FileTable.  
  
-   **BULK INSERT**  
  
    -   Eseguire una chiamata con la clausola **CHECK_CONSTRAINTS** .  
  
    -   Disabilitare lo spazio dei nomi FileTable ed eseguire una chiamata senza la clausola **CHECK_CONSTRAINTS** . Riabilitare quindi lo spazio dei nomi FileTable.  
  
-   **INSERT INTO ... SELECT \* FROM OPENROWSET(BULK ...)**  
  
    -   Eseguire una chiamata con la clausola **IGNORE_CONSTRAINTS** .  
  
    -   Disabilitare lo spazio dei nomi FileTable ed eseguire una chiamata senza la clausola **IGNORE_CONSTRAINTS** . Riabilitare quindi lo spazio dei nomi FileTable.  
  
 Per informazioni su come disabilitare i vincoli FileTable, vedere [Gestire le tabelle FileTable](../../relational-databases/blob/manage-filetables.md).  
  
###  <a name="disabling"></a> Procedura: Disabilitare vincoli FileTable per eseguire il caricamento bulk  
 Per eseguire il caricamento bulk di file in una tabella FileTable senza la necessità di applicare vincoli definiti dal sistema, è possibile disabilitare temporaneamente i vincoli. Per altre informazioni, vedere [Gestire le tabelle FileTable](../../relational-databases/blob/manage-filetables.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso a tabelle FileTable tramite Transact-SQL](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [Accedere alle tabelle FileTable con API di Input-Output dei file](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
  
  
