---
title: Supporto FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 75c5d2f0f04cf0692f4a6c6ca3145210fee014b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74308066"
---
# <a name="filestream-support"></a>Supporto FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  FILESTREAM consente di archiviare e accedere a valori binari di grandi dimensioni mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o accesso diretto al file system di Windows. Un valore binario di grandi dimensioni è un valore superiore a 2 gigabyte (GB). Per ulteriori informazioni sul supporto FILESTREAM migliorato, vedere [filestream &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md).  
  
 Quando si apre una connessione al database, ** \@ \@TEXTSIZE** verrà impostato su-1 ("Unlimited") per impostazione predefinita.  
  
 È anche possibile accedere alle colonne FILESTREAM e aggiornarle utilizzando l'API del file system di Windows.  
  
 Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [Supporto FILESTREAM &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [Supporto FILESTREAM &#40;&#41;ODBC](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [Accesso ai dati FILESTREAM con OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Esecuzione di una query sulle colonne FILESTREAM  
 I set di righe degli schemi in OLE DB non indicano se una colonna è di tipo FILESTREAM. Impossibile utilizzare ITableDefinition in OLE DB per creare una colonna FILESTREAM.  
  
 Le funzioni di catalogo come SQLColumns in ODBC non segnaleranno se una colonna è una colonna FILESTREAM.  
  
 Per creare colonne FILESTREAM o per individuare le colonne di tipo FILESTREAM esistenti, è possibile utilizzare la colonna **is_filestream** della vista di catalogo [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).  
  
 Di seguito è riportato un esempio:  
  
```  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>Compatibilità con le versioni precedenti  
 Se il client è stato compilato utilizzando la versione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di Native Client inclusa [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]in e l'applicazione si connette [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]a, il comportamento **varbinary (max)** sarà compatibile con. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Questo significa che i dati restituiti avranno come dimensione massima 2 GB. Per valori di dimensioni superiori a 2 GB, verrà eseguito un troncamento e restituito l'avviso "Troncamento a destra dei dati della stringa".  
  
 Quando la compatibilità con il tipo di dati è impostata su 80, il comportamento client sarà coerente con il comportamento del client legacy.  
  
 Per i client che utilizzano SQLOLEDB o altri provider rilasciati prima [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] della versione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di Native client, **varbinary (max)** verrà mappato all'immagine.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
