---
title: Aggiornamento dei dati in SQL Server i cursori | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 883eda7f0e1ed233f4c221c2afdb2236d3be2ca1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103483"
---
# <a name="updating-data-in-sql-server-cursors"></a>Aggiornamento dei dati nei cursori di SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Quando il recupero e l'aggiornamento dei dati tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursori, una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] applicazione consumer di Native Client OLE DB provider è associato mediante le stesse considerazioni e vincoli applicabili a qualsiasi altra applicazione client.  
  
 Solo le righe dei cursori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] partecipano al controllo di accesso ai dati simultaneo. Quando il consumer richiede un set di righe modificabile, il controllo della concorrenza viene effettuato da DBPROP_LOCKMODE. Per modificare il livello di controllo di accesso simultaneo, il consumer imposta la proprietà DBPROP_LOCKMODE prima di aprire il set di righe.  
  
 I livelli di isolamento della transazione possono provocare ritardi significativi nel posizionamento delle righe se la progettazione delle applicazioni client lascia aperte le transazioni per lunghi periodi di tempo. Per impostazione predefinita, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client utilizza il livello di isolamento read committed specificato da DBPROPVAL_TI_READCOMMITTED. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider supporta l'isolamento di lettura dirty quando la concorrenza di rowset è di sola lettura. In un set di righe modificabile il consumer può pertanto richiedere un livello di isolamento superiore ma non inferiore.  
  
## <a name="immediate-and-delayed-update-modes"></a>Modalità di aggiornamento immediato e posticipato  
 In modalità di aggiornamento immediato, ogni chiamata a **IRowsetChange::SetData** provoca un round trip al computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se il consumer apporta più modifiche a una sola riga, risulta più efficiente inviare tutte le modifiche con un'unica chiamata a **SetData**.  
  
 In modalità di aggiornamento posticipato, viene eseguito un round trip al computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ogni riga indicata nei parametri *cRows* e *rghRows* di **IRowsetUpdate::Update**.  
  
 In entrambe le modalità un round trip rappresenta una transazione distinta quando per il set di righe non è aperto alcun oggetto transazione.  
  
 Quando si utilizza **contrario**, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB provider tenta di elaborare ogni riga indicata. Errore si verifica a causa di valori di dati, lunghezza o stato non validi per tutte le righe non si arresta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client provider OLE DB di elaborazione. È possibile che vengano modificate tutte o nessuna delle altre righe che partecipano all'aggiornamento. Il consumer deve esaminare la *prgRowStatus* matrice per determinare l'errore per una specifica riga quando la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client restituisce DB_S_ERRORSOCCURRED.  
  
 Un consumer non deve presupporre che le righe vengano elaborate in base a un ordine specifico. Se un consumer richiede un'elaborazione ordinata di modifica dei dati su più di una riga, deve stabilire l'ordine nella logica dell'applicazione e aprire una transazione per includere il processo.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento dei dati nei set di righe](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
