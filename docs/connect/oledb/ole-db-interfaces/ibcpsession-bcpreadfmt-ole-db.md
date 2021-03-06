---
title: IBCPSession::BCPReadFmt (OLE DB Driver) | Microsoft Docs
description: Il metodo BCPReadFmt in OLE DB Driver per SQL Server legge i dati da un file di formato che specifica il formato dei dati nel file di dati.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- IBCPSession::BCPReadFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPReadFmt method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee5dd620981f2e41c20dd6a51c52c0b3d536a126
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081780"
---
# <a name="ibcpsessionbcpreadfmt-ole-db"></a>IBCPSession::BCPReadFmt (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Legge le informazioni sul formato per ogni colonna dal file di formato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT BCPReadFmt(   
      const wchar_t *pwszFormatFile);  
```  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo **BCPReadFmt** viene usato per la lettura di dati da un file di formato che specifica il formato dei dati nel file di dati. Questo metodo è in grado di rilevare la versione corretta del file di formato. Può rilevare automaticamente se il file è in formato xml o testo stile antico e comportarsi di conseguenza. La versione del file di formato supportata dal metodo BCP di OLE DB Driver per SQL Server è la 6.0 o successiva.  
  
 Dopo la lettura dei valori del formato, il metodo **BCPReadFmt** effettua le chiamate appropriate ai metodi [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) e [IBCPSession::BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md). L'utente può evitare di analizzare un file di formato ed effettuare queste chiamate.  
  
 Per salvare un file di formato, chiamare il metodo [IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md). Le chiamate al metodo **BCPReadFmt** possono fare riferimento ai formati salvati. In alternativa, l'utilità per la copia bulk (**bcp**) può salvare i formati di dati definiti dall'utente in file ai quali può fare riferimento il metodo **BCPReadFmt**.  
  
 Il valore **BCP_OPTION_DELAYREADFMT** del parametro *eOption* di [IBCPSession::BCPControl](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md) modifica il comportamento di IBCPSession::BCPReadFmt.  
  
## <a name="arguments"></a>Argomenti  
 *pwszFormatFile*[in]  
 Percorso e nome del file contenente i valori di formato per il file di dati.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 S_OK  
 Il metodo è riuscito.  
  
 E_FAIL  
 Si è verificato un errore specifico del provider. Per informazioni dettagliate, usare l'interfaccia [ISQLServerErrorInfo](./isqlservererrorinfo-geterrorinfo-ole-db.md).  
  
 E_OUTOFMEMORY  
 Errore di memoria insufficiente.  
  
 E_UNEXPECTED  
 La chiamata al metodo non era prevista. Non è stato ad esempio chiamato il metodo [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) prima della chiamata a questo metodo.  
  
## <a name="see-also"></a>Vedere anche  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Esecuzione di operazioni di copia bulk](../../oledb/features/performing-bulk-copy-operations.md)  
  
