---
title: Oggetti origine dati (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], data source objects
- SQL Server Native Client, data source objects
- SQLNCLI, data source objects
- SQL Server Native Client OLE DB provider, data source objects
- OLE DB data source objects [SQL Server Native Client]
- data source objects [OLE DB]
- CLSID
ms.assetid: c1d4ed20-ad3b-4e33-a26b-38d7517237b7
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2683cdc7762f1f500918edce436153e0130d04bd
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73758261"
---
# <a name="data-source-objects-ole-db"></a>Oggetti origine dati (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client utilizza il termine origine dati per il set di interfacce OLE DB utilizzate per stabilire un collegamento a un archivio dati, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La creazione di un'istanza dell'oggetto origine dati del provider è la prima attività di un consumer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Ogni provider OLE DB dichiara un identificatore di classe (CLSID) per se stesso. Il CLSID per il provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è il CLSID_SQLNCLI10 CC++ /GUID (il simbolo SQLNCLI_CLSID verrà risolto nel ProgID corretto nel file sqlncli. h a cui si fa riferimento). Con il CLSID, il consumer usa la funzione OLE **CoCreateInstance** per produrre un'istanza dell'oggetto origine dati.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è un server in-process. Le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti provider OLE DB di Native client vengono create utilizzando la macro CLSCTX_INPROC_SERVER per indicare il contesto eseguibile.  
  
 L'oggetto origine dati del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB espone le interfacce di inizializzazione OLE DB che consentono al consumer di connettersi ai database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esistenti.  
  
 Ogni connessione eseguita tramite il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client imposta automaticamente queste opzioni:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 In questo esempio viene utilizzata la macro identificatore di classe per creare un oggetto origine dati del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB e ottenere un riferimento all'interfaccia **IDBInitialize** .  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL, CLSCTX_INPROC_SERVER,  
    IID_IDBInitialize, (void**) &pIDBInitialize);  
  
if (SUCCEEDED(hr))  
{  
    //  Perform necessary processing with the interface.  
    pIDBInitialize->Uninitialize();  
    pIDBInitialize->Release();  
}  
else  
{  
    // Display error from CoCreateInstance.  
}  
```  
  
 Con la corretta creazione di un'istanza di un oggetto origine dati del provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client, l'applicazione consumer può continuare inizializzando l'origine dati e creando sessioni. Le sessioni OLE DB presentano le interfacce che consentono l'accesso ai dati e la relativa modifica.  
  
 Il provider di OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client effettua la prima connessione a un'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come parte di un'inizializzazione dell'origine dati completata correttamente. La connessione viene mantenuta a condizione che venga mantenuto un riferimento in una delle interfacce di inizializzazione dell'origine dati o fino a quando non viene chiamato il metodo **IDBInitialize::Uninitialize**.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Proprietà delle origini dati &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [Proprietà delle informazioni sulle origini dati](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [Proprietà di inizializzazione e di autorizzazione](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [Sessioni](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [Proprietà della sessione - Provider OLE DB di SQL Server Native Client](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [Oggetti di origine dati persistenti](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
