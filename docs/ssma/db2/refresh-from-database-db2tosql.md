---
title: Aggiornare dal Database (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ef7778854248f194c01254b9cd6f833f67e9cefc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270003"
---
# <a name="refresh-from-database-db2tosql"></a>Aggiornare dal Database (DB2ToSQL)
Il **aggiornare dal Database** nella finestra di dialogo consente di selezionare gli oggetti da aggiornare dal database di DB2. Le righe nella finestra di dialogo sono contraddistinte dal colore basato sullo stato dei metadati:  
  
-   Se i metadati dell'oggetto sono stato modificato in locale e nel database di DB2, la riga è blu.  
  
-   Se i metadati dell'oggetto sono stato modificato nel database di DB2, ma non in SSMA, la riga è gialla.  
  
-   Se i metadati dell'oggetto sono stato modificato in locale, ma non nel database di DB2, la riga è verde.  
  
-   Se l'oggetto è nuovo in database DB2, la riga è di colore rosa.  
  
È possibile specificare le impostazioni di aggiornamento di oggetti predefiniti in di **impostazioni del progetto** nella finestra di dialogo. Per altre informazioni, vedere [impostazioni del progetto&#40;sincronizzazione&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
Per l'accesso di **aggiornare dal Database** della finestra di dialogo scelta di un oggetto nel Visualizzatore metadati DB2 e fare clic su **aggiornare dal Database**.  
  
## <a name="options"></a>Opzioni  
**Comprimi (-)**  
Comprimi tutti i gruppi di oggetti per nascondere i singoli oggetti.  
  
**Expand (+)**  
Espandere tutti i gruppi di oggetti per mostrare i singoli oggetti.  
  
**Mostra/Nascondi oggetti uguali**  
Gli oggetti nell'elenco viene nascosto se i metadati degli oggetti sono lo stesso in database DB2 e in SSMA.  
  
**Aggiornare dal Database (freccia)**  
Utilizzare il pulsante freccia per specificare che i metadati per gli oggetti selezionati devono essere aggiornato in SSMA.  
  
**Eseguire l'operazione non aggiornato dal Database (pulsante) X**  
Utilizzare il pulsante X per specificare che i metadati per gli oggetti selezionati non devono essere aggiornati in SSMA.  
  
**Legenda**  
Consente di visualizzare una **legenda** nella finestra di dialogo. La legenda contiene il mapping tra i colori di riga e gli stati dei metadati.  
  
Per mantenere il **legenda** nella parte superiore della finestra di dialogo il **aggiornare dal Database** della finestra di dialogo Seleziona il **visualizzare nella parte superiore** casella di controllo.  
  
