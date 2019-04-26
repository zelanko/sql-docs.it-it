---
title: Progetto (sincronizzazione) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e223fb7d-05ec-4fa5-8973-d845c33a23dd
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: fe71e5b301c016e25bb179e0104831285dab3ce1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628687"
---
# <a name="project-settingssynchronization-oracletosql"></a>Impostazioni del progetto (sincronizzazione) (OracleToSQL)
La pagina di sincronizzazione del **impostazioni del progetto** finestra di dialogo contiene impostazioni che consentono di personalizzare la modalità SSMA carica e gli aggiornamenti di database oggetti, ad esempio tabelle e stored procedure, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Le opzioni di azioni predefinite specificano le impostazioni predefinite per l'aggiornamento di oggetti dal database Oracle e per la sincronizzazione degli oggetti con il database di SQL Server. Per altre informazioni, vedere [aggiornare dal Database - Oracle](../../ssma/oracle/refresh-from-database-oracletosql.md).  
  
È possibile accedere a due diverse pagine di sincronizzazione che contengono le stesse impostazioni:  
  
-   Per specificare le impostazioni per tutti i progetti SSMA futuri, nel **degli strumenti** menu, fare clic su **impostazioni di progetto predefinite**e quindi fare clic su **sincronizzazione** nella parte inferiore del riquadro di sinistra.  
  
-   Per specificare le impostazioni per il progetto corrente, il **strumenti** dal menu fare clic su **le impostazioni del progetto**e quindi fare clic su **sincronizzazione** nella parte inferiore del riquadro di sinistra.  
  
## <a name="miscellaneous-options"></a>Opzioni varie  
**Tentativi**  
Specifica il numero di tentativi di SSMA deve apportare durante il caricamento di oggetti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Gli oggetti che non vengono caricati nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel tentativo di corrente verrà ritentata fino a quando non SSMA raggiunge il numero massimo di tentativi durante il processo di sincronizzazione corrente. Viene impostato un valore predefinito **2**  
  
## <a name="synchronization-for-oracle-options"></a>Sincronizzazione per le opzioni di Oracle  
**Azione in caso di modifica di oggetti locali e remoti**  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando la definizione dell'oggetto viene modificato in SSMA e nel server di database. Viene impostato un valore predefinito **aggiornare dal database**.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
**Azione in caso di modifica oggetto locale**  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando l'oggetto viene modificato in SSMA. Viene impostato un valore predefinito **Skip**.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
**Azione in caso di modifica di oggetti remoti**  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando modificare gli oggetti nel server di database. Viene impostato un valore predefinito **aggiornare dal database**.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
**Azione quando i metadati degli oggetti locali sono mancanti**  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando mancano i metadati locali. Viene impostato un valore predefinito **aggiornare dal database**.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
## <a name="synchronization-for-sql-server-options"></a>Sincronizzazione per opzioni di SQL Server  
**Azione in caso di modifica di oggetti locali e remoti**  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando la definizione dell'oggetto viene modificato in SSMA e nel server di database. Viene impostato un valore predefinito **scrittura al database**.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **scrivere Database**, SSMA aggiornerà gli oggetti del database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
**Azione in caso di modifica oggetto locale**  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando l'oggetto viene modificato in SSMA. Viene impostato un valore predefinito **scrittura al database**.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **scrivere Database**, SSMA aggiornerà l'oggetto nel database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
**Azione in caso di modifica di oggetti remoti**  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando modificare gli oggetti nel server di database.  Viene impostato un valore predefinito **aggiornare dal database**.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA caricherà le definizioni di database nei metadati quando viene soddisfatta la condizione.  
  
-   Se si seleziona **scrivere Database**, SSMA aggiornerà l'oggetto nel database in base al contenuto dei metadati SSMA quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
**Azione quando i metadati degli oggetti locali sono mancanti**  
Specifica l'impostazione predefinita nella finestra di dialogo sincronizzazione quando mancano i metadati locali. Viene impostato un valore predefinito **aggiornare dal database**.  
  
-   Se si seleziona **aggiornare dal Database**, SSMA consente di selezionare la **aggiornare dal Database** opzione quando la condizione viene soddisfatta.  
  
-   Se si seleziona **scrivere Database**, SSMA eliminerà l'oggetto dal database quando viene soddisfatta la condizione.  
  
-   Se si seleziona **Skip**, SSMA non eseguirà alcuna azione di aggiornamento.  
  
