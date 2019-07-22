---
title: IRowsetFastLoad::InsertRow (OLE DB) | Microsoft Docs
description: IRowsetFastLoad::InsertRow (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IRowsetFastLoad::InsertRow (OLE DB)
apitype: COM
helpviewer_keywords:
- InsertRow method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b01c63e74ee26cea327a01e3bf9a3595bc5012d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015454"
---
# <a name="irowsetfastloadinsertrow-ole-db"></a>IRowsetFastLoad::InsertRow (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Aggiunge una riga al set di righe della copia bulk. Per gli esempi, vedere [copia dati bulk con &#40;IRowsetFastLoad&#41; OLE DB](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) e [inviare dati BLOB a SQL Server utilizzando IRowsetFastLoad e &#40;ISequentialStream&#41;OLE DB](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT InsertRow(  
      HACCESSOR hAccessor,  
      void* pData);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hAccessor*[in]  
 Handle della funzione di accesso che definisce i dati delle righe per la copia bulk. La funzione di accesso a cui viene fatto riferimento è una funzione di accesso di riga, che specifica l'associazione alla memoria del consumer contenente valori di dati.  
  
 *pData*[in]  
 Puntatore alla memoria del consumer contenente valori di dati. Per altre informazioni, vedere le [strutture DBBINDING](https://go.microsoft.com/fwlink/?LinkId=65955).  
  
## <a name="return-code-values"></a>Valori restituiti  
 S_OK  
 Il metodo è riuscito. I valori di stato associati per tutte le colonne hanno il valore DBSTATUS_S_OK o DBSTATUS_S_NULL.  
  
 E_FAIL  
 Si è verificato un errore. Le informazioni sull'errore sono disponibili nelle interfacce degli errori del set di righe.  
  
 E_INVALIDARG  
 L'argomento *pData* è stato impostato su un puntatore NULL.  
  
 E_OUTOFMEMORY  
 MSOLEDBSQL non è stato in grado di allocare memoria sufficiente per completare la richiesta.  
  
 E_UNEXPECTED  
 Il metodo è stato chiamato su un set di righe della copia bulk precedentemente invalidato dal metodo [IRowsetFastLoad::Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md).  
  
 DB_E_BADACCESSORHANDLE  
 L'argomento *hAccessor* specificato dal consumer non è valido.  
  
 DB_E_BADACCESSORTYPE  
 La funzione di accesso specificata non è una funzione di accesso di riga o non specifica la memoria del consumer.  
  
## <a name="remarks"></a>Remarks  
 Un errore di conversione dei dati del consumer nel tipo di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per una colonna causa la restituzione di E_FAIL da parte del driver OLE DB per SQL Server. I dati possono essere trasmessi a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con qualsiasi metodo **InsertRow** o solo con il metodo **Commit**. L'applicazione consumer può chiamare il metodo **InsertRow** diverse volte usando i dati errati prima di ricevere un avviso relativo all'errore di conversione del tipo di dati. Poiché il metodo **Commit** verifica che tutti i dati vengano specificati correttamente dal consumer, se necessario, il consumer può usare **Commit** in modo appropriato per convalidare i dati.  
  
 Il driver OLE DB per SQL Server set di righe della copia bulk sono di sola scrittura. Il driver OLE DB per SQL Server non espone metodi che consentono di eseguire query sul set di righe. Per terminare l'elaborazione, il consumer può rilasciare il riferimento all'interfaccia [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) senza chiamare il metodo **Commit**. Non sono disponibili funzioni per accedere alle righe inserite dal consumer nel set di righe e modificarne i valori o per rimuoverle singolarmente dal set di righe.  
  
 Le righe oggetto di copia bulk vengono formattate sul server per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Le opzioni eventualmente impostate per la connessione o per la sessione, ad esempio ANSI_PADDING, influiscono sul formato di riga. Per impostazione predefinita, questa opzione è impostata su per tutte le connessioni effettuate tramite il driver OLE DB per SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
 [OLE DB &#40;IRowsetFastLoad&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
