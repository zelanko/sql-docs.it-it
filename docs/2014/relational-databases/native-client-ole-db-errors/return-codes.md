---
title: Codici restituiti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 625d56a38d88b3cccbea1c75ad88917af1a6f6dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63228947"
---
# <a name="return-codes"></a>Codici restituiti
  Al livello più elementare, una funzione membro può avere esito positivo o negativo. A un livello più approfondito, una funzione può avere esito positivo, ma tale esito potrebbe non corrispondere alle previsioni dello sviluppatore dell'applicazione.  
  
 Per altre informazioni sui codici restituiti OLE DB, vedere [Codici restituiti (OLE DB)](https://go.microsoft.com/fwlink/?LinkId=101631).  
  
 Quando un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzione membro del provider OLE DB Native Client restituisce S_OK, la funzione ha avuto esito positivo.  
  
 Quando un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzione membro del provider OLE DB Native Client restituisce S_OK, le macro OLE/COM HRESULT FAILED e IS_ERROR possono determinare l'esito positivo o negativo complessivo di una funzione.  
  
 Se FAILED o IS_ERROR restituisce TRUE, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB Native Client ha la certezza che l'esecuzione della funzione membro non è riuscita. Se FAILED o IS_ERROR restituisce FALSE e il valore HRESULT diverso da S_OK, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB Native Client ha la certezza che la funzione ha avuto esito positivo in un certo senso. Il consumer può recuperare informazioni dettagliate su questo "esito positivo con informazioni" restituito dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfacce di errore del provider OLE DB Native Client. Inoltre, nel caso in cui una funzione non riesce in modo chiaro (la macro FAILED restituisce TRUE), informazioni dettagliate sull'errore sono disponibili dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfacce di errore del provider OLE DB Native Client.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Consumer del provider OLE DB per Client nativi verificano comunemente il valore restituito HRESULT DB_S_ERRORSOCCURRED "esito positivo con informazioni". Le funzioni membro che restituiscono DB_S_ERRORSOCCURRED definiscono in genere uno o più parametri che forniscono al consumer i valori di stato. Poiché è possibile che le uniche informazioni a disposizione del consumer siano quelle restituite nei parametri dei valori di stato, è necessario implementare la logica dell'applicazione per il recupero dei valori di stato quando essi sono disponibili.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzioni membro del provider OLE DB Native Client non restituiscono il codice di esito positivo S_FALSE. Tutti i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funzioni membro del provider OLE DB Native Client restituiscono sempre S_OK per indicare l'esito positivo.  
  
## <a name="see-also"></a>Vedere anche  
 [errori](errors.md)  
  
  
