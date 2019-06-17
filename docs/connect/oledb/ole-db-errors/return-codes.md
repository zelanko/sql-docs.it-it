---
title: Codici restituiti | Microsoft Docs
description: Codici restituiti
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- OLE DB Driver for SQL Server, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 7bb86d9e9c43b6d8c73f8018e80eebd5a0a54f5e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66786054"
---
# <a name="return-codes"></a>Codici restituiti
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Al livello più elementare, una funzione membro può avere esito positivo o negativo. A un livello più approfondito, una funzione può avere esito positivo, ma tale esito potrebbe non corrispondere alle previsioni dello sviluppatore dell'applicazione.  
  
 Per altre informazioni sui codici restituiti OLE DB, vedere [Codici restituiti (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando un Driver OLE DB per la funzione membro di SQL Server viene restituito S_OK, la funzione ha avuto esito positivo.  
  
 Quando una funzione membro del driver OLE DB per SQL Server non restituisce S_OK, le macro FAILED e IS_ERROR che decomprimono HRESULT OLE/COM possono determinare l'esito positivo o negativo complessivo di una funzione.  
  
 Se FAILED o IS_ERROR restituisce TRUE, il consumer del driver OLE DB per SQL Server ha la conferma dell'esito negativo dell'esecuzione della funzione membro. Se FAILED o IS_ERROR restituisce FALSE e il valore HRESULT non sia uguale a S_OK, il Driver OLE DB per SQL Server consumer è garantito la funzione ha avuto esito positivo in un certo senso. Il consumer può recuperare informazioni dettagliate su questa restituzione di "esito positivo con informazioni" dalle interfacce di errore del driver OLE DB per SQL Server. Anche nel caso in cui una funzione abbia un esito chiaramente negativo (la macro FAILED restituisce TRUE), le interfacce di errore del driver OLE DB per SQL Server rendono disponibili informazioni dettagliate sull'errore.  
  
 Driver OLE DB per i consumer di SQL Server verifica in genere il valore restituito HRESULT DB_S_ERRORSOCCURRED "esito positivo con informazioni". Le funzioni membro che restituiscono DB_S_ERRORSOCCURRED definiscono in genere uno o più parametri che forniscono al consumer i valori di stato. Poiché è possibile che le uniche informazioni a disposizione del consumer siano quelle restituite nei parametri dei valori di stato, è necessario implementare la logica dell'applicazione per il recupero dei valori di stato quando sono disponibili.  
  
 Il Driver OLE DB per le funzioni membro di SQL Server non restituiscono il codice di esito positivo S_FALSE. Tutti i Driver OLE DB per le funzioni membro di SQL Server restituiscono sempre S_OK per indicare l'esito positivo.  
  
## <a name="see-also"></a>Vedere anche  
 [errori](../../oledb/ole-db-errors/errors.md)  
  
  
