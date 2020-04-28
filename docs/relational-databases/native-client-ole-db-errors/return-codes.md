---
title: Codici restituiti | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB error handling, return codes
- SQL Server Native Client OLE DB provider, errors
- failed function [OLE DB]
- successful function [OLE DB]
- S_FALSE
- IS_ERROR macro
- DB_S_ERRORSOCCURRED return
- return codes [OLE DB]
- S_OK
- FAILED macro
- errors [OLE DB], return codes
ms.assetid: 7f7457e9-fce4-400c-82e5-ee02e9e811c6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09056c9d4964ad10b2b25f63ef5991a1a7742cab
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301025"
---
# <a name="return-codes"></a>Codici restituiti
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Al livello più elementare, una funzione membro può avere esito positivo o negativo. A un livello più approfondito, una funzione può avere esito positivo, ma tale esito potrebbe non corrispondere alle previsioni dello sviluppatore dell'applicazione.  
  
 Per altre informazioni sui codici restituiti OLE DB, vedere [Codici restituiti (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzione membro del provider OLE DB di Native Client restituisce S_OK, la funzione ha esito positivo.  
  
 Quando una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzione membro del provider OLE DB di Native client non restituisce S_OK, l'operazione di decompressione HRESULT OLE/com non è riuscita e IS_ERROR le macro possono determinare l'esito positivo o negativo complessivo di una funzione.  
  
 Se FAILED o IS_ERROR restituisce TRUE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB di Native client garantisce che l'esecuzione della funzione membro non sia riuscita. Se ha ESITo negativo o IS_ERROR restituisce FALSE e HRESULT non è uguale S_OK [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , il consumer del provider OLE DB di Native client ha la certezza che la funzione abbia avuto esito positivo. Il consumer può recuperare informazioni dettagliate su questo ritorno "success with information" dalle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfacce di errore del provider OLE DB di Native Client. Inoltre, nel caso in cui una funzione abbia esito negativo (la macro non riuscita restituisce TRUE), le informazioni estese [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sugli errori sono disponibili nelle interfacce di errore del provider OLE DB Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]I consumer del provider OLE DB di Native client in genere rilevano il DB_S_ERRORSOCCURRED HRESULT restituito "success with information". Le funzioni membro che restituiscono DB_S_ERRORSOCCURRED definiscono in genere uno o più parametri che forniscono al consumer i valori di stato. Poiché è possibile che le uniche informazioni a disposizione del consumer siano quelle restituite nei parametri dei valori di stato, è necessario implementare la logica dell'applicazione per il recupero dei valori di stato quando essi sono disponibili.  
  
 Le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzioni membro del provider OLE DB di Native client non restituiscono il codice di esito positivo S_FALSE. Tutte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le funzioni membro del provider OLE DB Native Client restituiscono sempre S_OK per indicare l'esito positivo.  
  
## <a name="see-also"></a>Vedere anche  
 [Errors](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
