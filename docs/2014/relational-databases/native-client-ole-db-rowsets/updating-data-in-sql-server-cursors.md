---
title: Aggiornamento dei dati nei cursori SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
ms.assetid: 732dafee-f2d5-4aef-aad7-3a8bf3b1e876
author: rothja
ms.author: jroth
ms.openlocfilehash: 42e6221a85c30e3adb97df3a11c9cbdc49216b4d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039117"
---
# <a name="updating-data-in-sql-server-cursors"></a>Aggiornamento dei dati nei cursori di SQL Server
  Quando si recuperano e si aggiornano i dati tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i cursori, un' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] applicazione consumer del provider OLE DB di Native Client è associata alle stesse considerazioni e ai vincoli che si applicano a qualsiasi altra applicazione client.  
  
 Solo le righe dei cursori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] partecipano al controllo di accesso ai dati simultaneo. Quando il consumer richiede un set di righe modificabile, il controllo della concorrenza viene effettuato da DBPROP_LOCKMODE. Per modificare il livello di controllo di accesso simultaneo, il consumer imposta la proprietà DBPROP_LOCKMODE prima di aprire il set di righe.  
  
 I livelli di isolamento della transazione possono provocare ritardi significativi nel posizionamento delle righe se la progettazione delle applicazioni client lascia aperte le transazioni per lunghi periodi di tempo. Per impostazione predefinita, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client utilizza il livello di isolamento Read Committed specificato da DBPROPVAL_TI_READCOMMITTED. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client supporta l'isolamento di lettura dirty quando la concorrenza del set di righe è di sola lettura. In un set di righe modificabile il consumer può pertanto richiedere un livello di isolamento superiore ma non inferiore.  
  
## <a name="immediate-and-delayed-update-modes"></a>Modalità di aggiornamento immediato e posticipato  
 In modalità di aggiornamento immediato, ogni chiamata a **IRowsetChange::SetData** provoca un round trip al computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se il consumer apporta più modifiche a una sola riga, risulta più efficiente inviare tutte le modifiche con un'unica chiamata a **SetData**.  
  
 In modalità di aggiornamento posticipato, viene eseguito un round trip al computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ogni riga indicata nei parametri *cRows* e *rghRows* di **IRowsetUpdate::Update**.  
  
 In entrambe le modalità un round trip rappresenta una transazione distinta quando per il set di righe non è aperto alcun oggetto transazione.  
  
 Quando si usa **IRowsetUpdate:: Update**, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native client tenta di elaborare ogni riga indicata. Si è verificato un errore a causa di dati non validi, lunghezza o valori di stato per una riga che non arresta l' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elaborazione del provider OLE DB di Native Client. È possibile che vengano modificate tutte o nessuna delle altre righe che partecipano all'aggiornamento. Il consumer deve esaminare la matrice *prgRowStatus* restituita per determinare l'esito negativo di una riga specifica quando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client restituisce DB_S_ERRORSOCCURRED.  
  
 Un consumer non deve presupporre che le righe vengano elaborate in base a un ordine specifico. Se un consumer richiede un'elaborazione ordinata di modifica dei dati su più di una riga, deve stabilire l'ordine nella logica dell'applicazione e aprire una transazione per includere il processo.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento dei dati dei set di righe](updating-data-in-rowsets.md)  
  
  
