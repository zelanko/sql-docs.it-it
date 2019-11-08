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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 36f376710dbcdd09daf664e9eee20533c5372641
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790229"
---
# <a name="return-codes"></a>Codici restituiti
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Al livello più elementare, una funzione membro può avere esito positivo o negativo. A un livello più approfondito, una funzione può avere esito positivo, ma tale esito potrebbe non corrispondere alle previsioni dello sviluppatore dell'applicazione.  
  
 Per altre informazioni sui codici restituiti OLE DB, vedere [Codici restituiti (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando una funzione membro del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB restituisce S_OK, la funzione ha esito positivo.  
  
 Quando una funzione membro del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB non restituisce S_OK, l'operazione di decompressione HRESULT OLE/COM non è riuscita e le macro IS_ERROR possono determinare l'esito positivo o negativo complessivo di una funzione.  
  
 Se ha ESITo negativo o IS_ERROR restituisce TRUE, il consumer del provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client garantisce che l'esecuzione della funzione membro non sia riuscita. Se ha ESITo negativo o IS_ERROR restituisce FALSE e HRESULT non è uguale S_OK, il consumer del provider OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client ha la certezza che la funzione abbia avuto esito positivo. Il consumer può recuperare informazioni dettagliate su questo ritorno "success with information" dalle interfacce di errore del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB. Inoltre, nel caso in cui una funzione abbia esito negativo (la macro non riuscita restituisce TRUE), le informazioni dettagliate sugli errori sono disponibili nelle interfacce di errore del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i consumer del provider OLE DB di Native Client incontrano in genere il DB_S_ERRORSOCCURRED HRESULT restituito "success with information". Le funzioni membro che restituiscono DB_S_ERRORSOCCURRED definiscono in genere uno o più parametri che forniscono al consumer i valori di stato. Poiché è possibile che le uniche informazioni a disposizione del consumer siano quelle restituite nei parametri dei valori di stato, è necessario implementare la logica dell'applicazione per il recupero dei valori di stato quando essi sono disponibili.  
  
 Le funzioni membro del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB non restituiscono il codice di esito positivo S_FALSE. Tutte le funzioni membro del provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB restituiscono sempre S_OK per indicare l'esito positivo.  
  
## <a name="see-also"></a>Vedere anche  
 [errori](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
