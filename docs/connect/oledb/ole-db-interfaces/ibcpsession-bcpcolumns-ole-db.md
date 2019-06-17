---
title: 'Ibcpsession:: BCPColumns (OLE DB) | Microsoft Docs'
description: IBCPSession::BCPColumns (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPColumns (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColumns method
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 0be5ef8671e327601314061902b804decc9ecc7a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790950"
---
# <a name="ibcpsessionbcpcolumns-ole-db"></a>IBCPSession::BCPColumns (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Imposta il numero di campi da associare alle colonne di una tabella di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT BCPColumns(   
      DBCOUNTITEM nColumns);  
```  
  
## <a name="remarks"></a>Remarks  
 Chiama internamente [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) per impostare i valori predefiniti per i dati dei campi. Questi valori predefiniti vengono ottenuti dalle informazioni sulle colonne di SQL Server recuperate internamente dal provider quando si specifica il nome di tabella tramite [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md).  
  
> [!NOTE]  
>  È possibile chiamare questo metodo solo dopo avere chiamato **BCPInit** con un nome di file valido.  
  
 È consigliabile chiamare questo metodo solo se si intende utilizzare un formato di file utente diverso da quello predefinito. Per ulteriori informazioni su una descrizione del formato di file utente predefinito, vedere il metodo **BCPInit**.  
  
 Dopo avere chiamato il metodo **BCPColumns**, è necessario chiamare il metodo **BCPColFmt** per ogni colonna del file utente per definire in modo completo un formato di file personalizzato.  
  
## <a name="arguments"></a>Argomenti  
 *nColumns*[in]  
 Numero totale di campi nel file utente. Anche se si prepara la copia bulk dei dati dal file utente in una tabella di SQL Server e non si prevede di copiare tutti i campi del file utente, è comunque necessario impostare l'argomento *nColumns* sul numero totale di campi del file utente. I campi ignorati possono quindi essere specificati tramite **BCPColFmt**.  
  
## <a name="return-code-values"></a>Valori restituiti  
 S_OK  
 Il metodo è riuscito.  
  
 E_FAIL  
 Si è verificato un errore specifico del provider. Per informazioni dettagliate, usare l'interfaccia [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).  
  
 E_UNEXPECTED  
 La chiamata al metodo non era prevista. Non è stato ad esempio chiamato il metodo **BCPInit** prima della chiamata a questo metodo. Si verifica inoltre quando questo metodo viene chiamato più volte per un'operazione di copia bulk.  
  
 E_OUTOFMEMORY  
 Errore di memoria insufficiente.  
  
## <a name="see-also"></a>Vedere anche  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Esecuzione di operazioni di copia bulk](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
