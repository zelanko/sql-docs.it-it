---
title: Aggiornare dal database (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59a6db8f-2db6-4071-9005-928a7231de92
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 690d12a2f5f397256760c1c0cf5e2ee954d90843
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62473897"
---
# <a name="refresh-from-database-mysqltosql"></a>Eseguire l'aggiornamento dal database (MySQLToSQL)
Il **aggiornare dal Database** nella finestra di dialogo consente di selezionare gli oggetti da aggiornare dal database di MySQL. Le righe nella finestra di dialogo sono contraddistinte dal colore basato sullo stato dei metadati:  
  
-   Se i metadati dell'oggetto sono stato modificato in locale e nel database MySQL, la riga è blu.  
  
-   Se i metadati dell'oggetto sono stato modificato nel database MySQL, ma non in SSMA, la riga è gialla.  
  
-   Se i metadati dell'oggetto sono stato modificato in locale, ma non nel database di MySQL, la riga è verde.  
  
-   Se l'oggetto è una novità di database MySQL, la riga è di colore rosa.  
  
È possibile specificare le impostazioni di aggiornamento di oggetti predefiniti in di **impostazioni del progetto** nella finestra di dialogo. Per altre informazioni, vedere [impostazioni del progetto &#40;sincronizzazione&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
Per l'accesso di **aggiornare dal Database** della finestra di dialogo scelta di un oggetto nel Visualizzatore metadati MySQL e fare clic su **aggiornare dal Database**.  
  
## <a name="options"></a>Opzioni  
  
|||  
|-|-|  
|**Nome**|**Definizione**|  
|**Comprimi (-)**|Comprimi tutti i gruppi di oggetti per nascondere i singoli oggetti.|  
|**Expand (+)**|Espandere tutti i gruppi di oggetti per mostrare i singoli oggetti.|  
|**Mostra/Nascondi oggetti uguali**|Gli oggetti nell'elenco viene nascosto se i metadati degli oggetti sono lo stesso nel database MySQL in SSMA.|  
|**Aggiornare dal Database (freccia)**|Utilizzare il pulsante freccia per specificare che i metadati per gli oggetti selezionati devono essere aggiornato in SSMA.|  
|**Eseguire l'operazione non aggiornato dal Database (pulsante) X**|Utilizzare il pulsante X per specificare che i metadati per gli oggetti selezionati non devono essere aggiornati in SSMA.|  
|**Legenda**|Consente di visualizzare una **legenda** nella finestra di dialogo. La legenda contiene il mapping tra i colori di riga e gli stati dei metadati.<br /><br />Per mantenere il **legenda** nella parte superiore della finestra di dialogo il **aggiornare dal Database** della finestra di dialogo Seleziona il **visualizzare nella parte superiore** casella di controllo.|  
  
