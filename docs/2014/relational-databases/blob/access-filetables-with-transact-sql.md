---
title: Accedere a tabelle FileTable tramite Transact-SQL| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with T-SQL
ms.assetid: 3c4a5ffb-c521-4696-99cb-2b03cffc9c02
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b56bba0567a96b7bdd7b75ad191d553ffa019930
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66010432"
---
# <a name="access-filetables-with-transact-sql"></a>Accesso a tabelle FileTable tramite Transact-SQL
  Viene descritto il funzionamento dei comandi [!INCLUDE[tsql](../../includes/tsql-md.md)] DML (Data Manipulation Language) con una tabella FileTable.  
  
##  <a name="BasicsInsert"></a> Operazioni INSERT in tabelle FileTable  
 Le considerazioni seguenti si applicano alle operazioni **INSERT** in tabelle FileTable:  
  
-   Tutte le colonne di attributi dei file dispongono di vincoli NOT NULL. Se i valori non sono impostati in modo esplicito, vengono forniti valori predefiniti appropriati.  
  
-   Se l'istruzione INSERT imposta **name**, **path_locator**, **parent_path_locator**o gli attributi del file, verranno applicati vincoli definiti dal sistema.  
  
-   L'applicazione può ottenere **path_locator** per un file o una directory passando il percorso del file system alla funzione [GetPathLocator &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql).  
  
##  <a name="BasicsUpdate"></a> Operazioni UPDATE in tabelle FileTable  
 Le considerazioni seguenti si applicano alle operazioni **UPDATE** in tabelle FileTable:  
  
-   Sono consentiti aggiornamenti a tutti i dati definiti dall'utente.  
  
-   Se l'istruzione INSERT imposta **name**, **path_locator**, **parent_path_locator**o gli attributi del file, verranno applicati vincoli definiti dal sistema.  
  
-   Gli aggiornamenti possono essere effettuati sui dati FILESTREAM nella colonna **file_stream** senza influire su alcune delle altre colonne, compresi i timestamp.  
  
##  <a name="BasicsDelete"></a> Operazioni DELETE in tabelle FileTable  
 Le considerazioni seguenti si applicano alle operazioni **DELETE** in tabelle FileTable:  
  
-   L'eliminazione di una riga comporta la rimozione del file o della directory corrispondente dal file system.  
  
-   L'eliminazione di una riga non riesce se la riga corrisponde a una directory che contiene altri file o directory.  
  
##  <a name="BasicsConstraints"></a> Vincoli applicati per operazioni DML in tabelle FileTable  
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
 [Caricamento di file in FileTable](load-files-into-filetables.md)   
 [Work with Directories and Paths in FileTables](work-with-directories-and-paths-in-filetables.md)   
 [Accedere alle tabelle FileTable con API di Input-Output dei file](access-filetables-with-file-input-output-apis.md)   
 [DDL, funzioni, stored procedure e viste FileTable](../views/views.md)  
  
  
