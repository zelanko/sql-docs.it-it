---
title: (Caricamento oggetti) Impostazioni progetto (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9ec1c1e8-a3e1-4e81-bf49-631f87daa209
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c8aebc643d3d313dcf97bbe69044ee795649ba46
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929421"
---
# <a name="project-settings-loading-objects-accesstosql"></a>(Caricamento oggetti) Impostazioni progetto (AccessToSQL)
Le impostazioni del progetto di caricamento di oggetti consentono di configurare come accedere agli oggetti di database è sincronizzati con gli oggetti di database di SQL Server.  
  
Le azioni predefinite specificano le impostazioni predefinite per l'aggiornamento di oggetti dal database di Access e per la sincronizzazione degli oggetti con il database di SQL Server. Per altre informazioni, vedere [aggiornare dal Database &#40;AccessToSQL&#41;](../../ssma/access/refresh-from-database-accesstosql.md)  
  
È possibile accedere a due diverse pagine di sincronizzazione che contengono le stesse impostazioni:  
  
-   Per specificare le impostazioni per tutti i progetti SSMA futuri, nel **Tools** menu, fare clic su **impostazioni DefaultProject**e quindi fare clic su **il caricamento di oggetti** nella parte inferiore del riquadro di sinistra.  
  
-   Per specificare le impostazioni per il progetto corrente, il **strumenti** dal menu fare clic su **le impostazioni del progetto**e quindi fare clic su **il caricamento di oggetti** nella parte inferiore del riquadro di sinistra.  
  
## <a name="options"></a>Opzioni  
  
##### <a name="misc"></a>Varie  
  
##### <a name="attempts"></a>Tentativi  
Fornisce le informazioni sul numero di passaggi necessarie per caricare in SQL Server. Caricamento degli oggetti in SQL Server viene in genere eseguito in più passaggi. Gli oggetti che non è possibile caricare il primo passaggio, ad esempio le chiavi esterne, potrebbero essere caricato correttamente durante il passaggio successivo.  
  
Il valore predefinito è 2.  
  
## <a name="synchronization-for-sql-server"></a>Sincronizzazione per SQL Server  
  
##### <a name="default-action-on-local-and-remote-object-change"></a>Azione predefinita in caso di modifica oggetto locale e remota  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando la definizione dell'oggetto viene modificato in SSMA e nel server di database.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **scrivere Database**, SSMA aggiornerà gli oggetti del database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
##### <a name="default-action-on-local-object-change"></a>Azione predefinita in caso di modifica oggetto locale  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando l'oggetto viene modificato in SSMA.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **scrivere Database**, SSMA aggiornerà l'oggetto nel database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
##### <a name="default-action-on-remote-object-change"></a>Azione predefinita in caso di modifica di oggetti remoti  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando modificare gli oggetti nel server di database.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **scrivere Database**, SSMA aggiornerà l'oggetto nel database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
##### <a name="default-action-when-local-object-metadata-is-missing"></a>Azione predefinita quando mancano i metadati di oggetto locale  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando mancano i metadati locali.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA consente di selezionare l'aggiornamento dall'opzione di Database quando viene soddisfatta la condizione.  
  
-   Se si seleziona **scrivere Database**, SSMA eliminerà l'oggetto dal database quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
