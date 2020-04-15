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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301025"
---
# <a name="return-codes"></a>Codici restituiti
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Al livello più elementare, una funzione membro può avere esito positivo o negativo. A un livello più approfondito, una funzione può avere esito positivo, ma tale esito potrebbe non corrispondere alle previsioni dello sviluppatore dell'applicazione.  
  
 Per altre informazioni sui codici restituiti OLE DB, vedere [Codici restituiti (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una funzione membro del provider OLE DB di Native Client restituisce S_OK, la funzione ha avuto esito positivo.  
  
 Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una funzione membro del provider OLE DB di Native Client non restituisce S_OK, le macro OLE/COM HRESULT-unpacking non riuscita e IS_ERROR possono determinare l'esito positivo o negativo complessivo di una funzione.  
  
 Se FAILED o IS_ERROR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce TRUE, il consumer del provider OLE DB Native Client è certo che l'esecuzione della funzione membro non è riuscita. Se FAILED o IS_ERROR restituiscono FALSE e HRESULT non è uguale S_OK, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB Native Client è certo che la funzione ha avuto esito positivo in un certo senso. Il consumer può recuperare informazioni dettagliate su questo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "successo con informazioni" restituite dalle interfacce di errore del provider OLE DB Native Client. Inoltre, nel caso in cui una funzione non riesca chiaramente (la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] macro FAILED restituisce TRUE), le informazioni estese sugli errori sono disponibili dalle interfacce di errore del provider OLE DB di Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]I consumer del provider OLE DB Native Client incontrano in genere il DB_S_ERRORSOCCURRED restituito HRESULT "successo con le informazioni". Le funzioni membro che restituiscono DB_S_ERRORSOCCURRED definiscono in genere uno o più parametri che forniscono al consumer i valori di stato. Poiché è possibile che le uniche informazioni a disposizione del consumer siano quelle restituite nei parametri dei valori di stato, è necessario implementare la logica dell'applicazione per il recupero dei valori di stato quando essi sono disponibili.  
  
 Le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzioni membro del provider OLE DB Native Client non restituiscono il codice di esito positivo S_FALSE. Tutte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le funzioni membro del provider OLE DB Native Client restituiscono sempre S_OK per indicare l'esito positivo.  
  
## <a name="see-also"></a>Vedere anche  
 [Errors](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
