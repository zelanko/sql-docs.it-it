---
title: Impostazioni (sincronizzazione) (MySQLToSQL) del progetto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e82fa9d02fdbfe876f4097c54c6877c3a3a81fee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62473907"
---
# <a name="project-settings-synchronization-mysqltosql"></a>Impostazioni del progetto (sincronizzazione) (MySQLToSQL)
La sincronizzazione **impostazioni del progetto** consentono di configurare la modalità di sincronizzazione degli oggetti di database MySQL con gli oggetti di database di SQL Server.  
  
Le azioni predefinite specificano le impostazioni predefinite per l'aggiornamento di oggetti dal database di MySQL e per la sincronizzazione degli oggetti con il database di SQL Server. Per altre informazioni, vedere [aggiornare dal database &#40;MySQLToSQL&#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
È possibile accedere a due diverse pagine di sincronizzazione che contengono le stesse impostazioni:  
  
-   Per specificare le impostazioni per tutti i progetti SSMA futuri, nelle **degli strumenti** menu, fare clic su **DefaultProject impostazioni**e quindi fare clic su **sincronizzazione** nella parte inferiore del riquadro di sinistra.  
  
-   Per specificare le impostazioni per il progetto corrente, il **strumenti** dal menu fare clic su **le impostazioni del progetto**e quindi fare clic su **sincronizzazione** nella parte inferiore del riquadro di sinistra.  
  
## <a name="options"></a>Opzioni  
  
##### <a name="misc"></a>Varie  
  
##### <a name="attempts"></a>Tentativi  
Fornisce le informazioni sul numero di passaggi necessarie per caricare in SQL Server. Caricamento degli oggetti in SQL Server viene in genere eseguito in più passaggi. Gli oggetti che non è possibile caricare il primo passaggio, ad esempio le chiavi esterne, potrebbero essere caricato correttamente durante il passaggio successivo.  
  
Il valore predefinito è 2.  
  
## <a name="synchronization-for-mysql"></a>Sincronizzazione per MySQL  
  
##### <a name="action-on-local-and-remote-object-change"></a>Azione in caso di modifica di oggetti locali e remoti  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando la definizione dell'oggetto viene modificato in SSMA e nel server di database.  
  
-   Se si seleziona l'aggiornamento dal Database, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona Skip, SSMA non eseguirà alcuna azione di aggiornamento.  
  
##### <a name="action-on-local-object-change"></a>Azione in caso di modifica oggetto locale  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando l'oggetto viene modificato in SSMA.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
##### <a name="action-on-remote-object-change"></a>Azione in caso di modifica di oggetti remoti  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando modificare gli oggetti nel server di database.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Azione quando i metadati degli oggetti locali sono mancanti  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando i metadati locali sono mancanti.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento  
  
## <a name="synchronization-for-sql-server"></a>Sincronizzazione per SQL Server  
  
##### <a name="action-on-local-and-remote-object-change"></a>Azione in caso di modifica oggetto locale e remota  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando la definizione dell'oggetto viene modificato in SSMA e nel server di database.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **scrivere Database**, SSMA aggiornerà gli oggetti del database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
##### <a name="action-on-local-object-change"></a>Azione in caso di modifica oggetto locale  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando l'oggetto viene modificato in SSMA.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **scrivere Database**, SSMA aggiornerà l'oggetto nel database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
##### <a name="action-on-remote-object-change"></a>Azione in caso di modifica di oggetti remoti  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando modificare gli oggetti nel server di database.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **scrivere Database**, SSMA aggiornerà l'oggetto nel database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Azione quando i metadati degli oggetti locali sono mancanti  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando mancano i metadati locali.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA consente di selezionare l'aggiornamento dall'opzione di Database quando viene soddisfatta la condizione.  
  
-   Se si seleziona **scrivere Database**, SSMA eliminerà l'oggetto dal database quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
