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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bf8ddb4e3794c8ad7889f395726fb325e071deb3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303868"
---
# <a name="filestream-support"></a>Supporto FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  FILESTREAM consente di archiviare e accedere a valori binari di grandi dimensioni mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o accesso diretto al file system di Windows. Un valore binario di grandi dimensioni è un valore superiore a 2 gigabyte (GB). Per altre informazioni sul supporto FILESTREAM avanzato, vedere [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md).  
  
 Quando viene aperta una connessione al database, ** \@ \@TEXTSI-E** verrà impostato su -1 ("illimitato"), per impostazione predefinita.  
  
 È anche possibile accedere alle colonne FILESTREAM e aggiornarle utilizzando l'API del file system di Windows.  
  
 Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [Supporto FILESTREAM &#40;&#41;OLE DB](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [Supporto FILESTREAM &#40;&#41;ODBC](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [Accesso ai dati FILESTREAM con OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Esecuzione di una query sulle colonne FILESTREAM  
 I set di righe degli schemi in OLE DB non indicano se una colonna è di tipo FILESTREAM. Impossibile utilizzare ITableDefinition in OLE DB per creare una colonna FILESTREAM.  
  
 Le funzioni di catalogo, ad esempio SQLColumns in ODBC, non segnalano se una colonna è una colonna FILESTREAM.  
  
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
 Se il client è stato [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compilato utilizzando la [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]versione di Native [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]Client inclusa in , e l'applicazione si connette a , il comportamento **varbinary(max)** sarà compatibile con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Questo significa che i dati restituiti avranno come dimensione massima 2 GB. Per valori di dimensioni superiori a 2 GB, verrà eseguito un troncamento e restituito l'avviso "Troncamento a destra dei dati della stringa".  
  
 Quando la compatibilità con il tipo di dati è impostata su 80, il comportamento client sarà coerente con il comportamento del client legacy.  
  
 Per i client che utilizzano SQLOLEDB [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] altri provider rilasciati prima della versione di Native Client, **varbinary(max)** verrà mappato all'immagine.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
