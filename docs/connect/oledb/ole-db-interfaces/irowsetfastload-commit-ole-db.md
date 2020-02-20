---
title: IRowsetFastLoad::Commit (OLE DB) | Microsoft Docs
description: IRowsetFastLoad::Commit (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IRowsetFastLoad::Commit (OLE DB)
apitype: COM
helpviewer_keywords:
- Commit method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: d76ad5dc881ab4f31808d738d9beacd85929d279
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994405"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Contrassegna la fine di un batch di righe inserite e scrive le righe nella tabella di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per gli esempi, vedere [Eseguire una copia bulk dei dati usando IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md) e [Inviare dati BLOB a SQL Server usando IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT Commit(  
      BOOL fDone);  
```  
  
## <a name="arguments"></a>Argomenti  
 *fDone*[in]  
 Se impostato su FALSE, il set di righe resta valido e può essere utilizzato dal consumer per l'inserimento di altre righe. Se impostato su TRUE, il set di righe non è più valido e il consumer non può inserire altre righe.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 S_OK  
 Il metodo è riuscito e tutti i dati inseriti sono stati scritti nella tabella [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 E_FAIL  
 Si è verificato un errore specifico del provider. Recuperare informazioni relative al testo dell'errore specifico dal provider.  
  
 E_UNEXPECTED  
 Il metodo è stato chiamato su un set di righe della copia bulk precedentemente invalidato dal metodo **IRowsetFastLoad::Commit**.  
  
## <a name="remarks"></a>Osservazioni  
 Un set di righe della copia bulk di OLE DB Driver per SQL Server si comporta come un set di righe in modalità di aggiornamento ritardato. Quando l'utente inserisce dati di riga nel set di righe, le righe inserite vengono gestite analogamente agli inserimenti in sospeso di un set di righe che supporta **IRowsetUpdate**.  
  
 Il consumer deve chiamare il metodo **Commit** sul set di righe della copia bulk per scrivere le righe inserite nella tabella [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esattamente come quando si usa il metodo **IRowsetUpdate::Update** per inviare le righe in sospeso a un'istanza di SQL Server.  
  
 Se il consumer rilascia il riferimento al set di righe della copia bulk senza chiamare il metodo **Commit**, tutte le righe inserite e non scritte in precedenza andranno perse.  
  
 Il consumer può raggruppare le righe inserite chiamando il metodo **Commit** con l'argomento *fDone* impostato su FALSE. Quando *fDone* è impostato su TRUE, il set di righe non è più valido. Un set di righe della copia bulk non valido supporta solo l'interfaccia **ISupportErrorInfo** e il metodo **IRowsetFastLoad::Release**.  
  
## <a name="see-also"></a>Vedere anche  
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)  
  
  
