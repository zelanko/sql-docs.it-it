---
title: Accedere a tabelle FileTable tramite Transact-SQL| Microsoft Docs
description: Informazioni sul funzionamento dei comandi Transact-SQL DML (Data Manipulation Language) con una tabella FileTable. Vedere quali vincoli definiti dal sistema vengono applicati durante le operazioni DML.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with T-SQL
ms.assetid: 3c4a5ffb-c521-4696-99cb-2b03cffc9c02
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f6b0b0d1f7dd6467487266206756af8f82c66bf4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85744400"
---
# <a name="access-filetables-with-transact-sql"></a>Accesso a tabelle FileTable tramite Transact-SQL
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Viene descritto il funzionamento dei comandi [!INCLUDE[tsql](../../includes/tsql-md.md)] DML (Data Manipulation Language) con una tabella FileTable.  
  
##  <a name="insert-operations-on-filetables"></a><a name="BasicsInsert"></a> Operazioni INSERT in tabelle FileTable  
 Le considerazioni seguenti si applicano alle operazioni **INSERT** in tabelle FileTable:  
  
-   Tutte le colonne di attributi dei file dispongono di vincoli NOT NULL. Se i valori non sono impostati in modo esplicito, vengono forniti valori predefiniti appropriati.  
  
-   Se l'istruzione INSERT imposta **name**, **path_locator**, **parent_path_locator**o gli attributi del file, verranno applicati vincoli definiti dal sistema.  
  
-   L'applicazione può ottenere **path_locator** per un file o una directory passando il percorso del file system alla funzione [GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md).  
  
##  <a name="update-operations-on-filetables"></a><a name="BasicsUpdate"></a> Operazioni UPDATE in tabelle FileTable  
 Le considerazioni seguenti si applicano alle operazioni **UPDATE** in tabelle FileTable:  
  
-   Sono consentiti aggiornamenti a tutti i dati definiti dall'utente.  
  
-   Se l'istruzione INSERT imposta **name**, **path_locator**, **parent_path_locator**o gli attributi del file, verranno applicati vincoli definiti dal sistema.  
  
-   Gli aggiornamenti possono essere effettuati sui dati FILESTREAM nella colonna **file_stream** senza influire su alcune delle altre colonne, compresi i timestamp.  
  
##  <a name="delete-operations-on-filetables"></a><a name="BasicsDelete"></a> Operazioni DELETE in tabelle FileTable  
 Le considerazioni seguenti si applicano alle operazioni **DELETE** in tabelle FileTable:  
  
-   L'eliminazione di una riga comporta la rimozione del file o della directory corrispondente dal file system.  
  
-   L'eliminazione di una riga non riesce se la riga corrisponde a una directory che contiene altri file o directory.  
  
##  <a name="constraints-that-are-enforced-for-dml-operations-on-filetables"></a><a name="BasicsConstraints"></a> Vincoli applicati per operazioni DML in tabelle FileTable  
 I vincoli referenziali/univoci definiti dal sistema garantiscono che le azioni DML non danneggino l'integrità della gerarchia dello spazio dei nomi. I vincoli applicati includono gli elementi seguenti:  
  
-   Quando si imposta o si modifica il **nome** del file o della directory:  
  
    -   Vengono applicate le convenzioni di denominazione di Windows per file e directory.  
  
    -   Verrà applicata l'univocità del nome nella directory padre.  
  
-   Quando si imposta o modifica il percorso di un file o di una directory impostando o modificando **path_locator** o **parent_path_locator**:  
  
    -   Viene applicata l'univocità.  
  
    -   Viene applicata la consistenza dell'albero gerarchico di directory e file, inclusa la coerenza dei valori **path_locator** e **parent_path_locator** .  
  
-   Non è possibile impostare il valore **is_directory** su true mentre la colonna **file_stream** è impostata su non Null. I dati nella colonna **file_stream** indicano che la riga rappresenta un file e non una directory.  
  
-   Le colonne degli attributi di file non possono essere Null. I vincoli NOT NULL vengono applicati con i valori predefiniti.  
  
-   Il valore di **last_access_time** non può essere precedente a **last_write_time** e **creation_time**.  
  
## <a name="see-also"></a>Vedere anche  
 [Caricamento di file in FileTable](../../relational-databases/blob/load-files-into-filetables.md)   
 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [Accedere alle tabelle FileTable con API di Input-Output dei file](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)   
 [DDL, funzioni, stored procedure e viste FileTable](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
