---
title: Proprietà origine dati (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 6e14fefc-4e0b-4847-a833-4cf0abe65d50
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 50a5f3ba0a306f2c170e62965b84074592387c25
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73774686"
---
# <a name="data-source-properties-ole-db"></a>Proprietà delle origini dati (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa le proprietà dell'origine dati come indicato di seguito.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|L/S: Lettura/scrittura Impostazione predefinita: Nessuna<br /><br /> Descrizione: il valore di DBPROP_CURRENTCATALOG segnala il database corrente per una sessione del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB Native Client. Se si imposta il valore della proprietà, si ottiene lo stesso effetto che si ottiene impostando il database corrente utilizzando l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] USE *database*.<br /><br /> A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], se si chiama [sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) e si specifica il nome del database in caratteri minuscoli, anche se il database è stato creato usando sia maiuscole che minuscole, DBPROP_CURRENTCATALOG restituirà il nome in minuscolo. Con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], DBPROP_CURRENTCATALOG restituisce invece la combinazione di maiuscole e minuscole prevista.|  
|DBPROP_MULTIPLECONNECTIONS|L/S: Lettura/scrittura Impostazione predefinita: VARIANT_FALSE<br /><br /> Descrizione: Se la connessione esegue un comando che non produce un set di righe o produce un set di righe che non è un cursore server e si esegue un altro comando, verrà creata una nuova connessione per eseguire il nuovo comando se DBPROP_MULTIPLECONNECTIONS è VARIANT_TRUE.<br /><br /> Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client non creerà un'altra connessione se DBPROP_MULTIPLECONNECTION è VARIANT_FALSE o se una transazione è attiva nella connessione. Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client restituisce DB_E_OBJECTOPEN se DBPROP_MULTIPLECONNECTIONS è VARIANT_FALSE e restituisce E_FAIL se è presente una transazione attiva. Le transazioni e il blocco vengono gestiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per singola connessione. Se viene generata una seconda connessione, i comandi sulle connessioni separate non condividono blocchi. Per assicurarsi che un comando non blocchi un altro comando, mantenere attivi i blocchi sulle righe richieste da quest'ultimo. Ciò vale anche nel caso di creazione di più sessioni.<br /><br /> Ogni sessione ha una connessione separata.|  
  
 Nel set di proprietà specifico del provider DBPROPSET_SQLSERVERDATASOURCE, il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB Native Client definisce le seguenti proprietà dell'origine dati aggiuntive.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|L/S: Lettura/scrittura Impostazione predefinita: VARIANT_FALSE<br /><br /> Descrizione: Per abilitare la copia bulk dalla memoria, la proprietà SSPROP_ENABLEFASTLOAD deve essere impostata su VARIANT_TRUE. Se questa proprietà è impostata sull'origine dati, la sessione appena creata consente al consumer di accedere all'interfaccia [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md).<br /><br /> Se la proprietà è impostata su VARIANT_TRUE, l'interfaccia **IRowsetFastLoad** è disponibile attraverso **IOpenRowset::OpenRowset** richiedendo l'interfaccia **IID_IRowsetFastLoad** o impostando **SSPROP_IRowsetFastLoad** su VARIANT_TRUE.|  
|SSPROP_ENABLEBULKCOPY|L/S: Lettura/scrittura Impostazione predefinita: VARIANT_FALSE<br /><br /> Descrizione: Per abilitare la copia bulk dai file, la proprietà SSPROP_ENABLEBULKCOPY deve essere impostata su VARIANT_TRUE. Se questa proprietà è impostata sull'origine dati, l'accesso del consumer all'interfaccia IBCPSession è disponibile allo stesso livello delle sessioni.<br /><br /> Anche SSPROP_IRowsetFastLoad deve essere impostato su VARIANT_TRUE.|  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetti &#40;origine dati OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
