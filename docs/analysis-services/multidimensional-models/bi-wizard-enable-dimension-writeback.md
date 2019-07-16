---
title: Abilitazione writeback della dimensione | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 561dc878302afe7636a2660a9e194ac14a35c7f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68179111"
---
# <a name="bi-wizard---enable-dimension-writeback"></a>Procedura guidata per BI - Abilitare il writeback della dimensione
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Aggiungere a un cubo o a una dimensione la funzionalità avanzata di writeback della dimensione per consentire agli utenti di modificare manualmente la struttura e i membri della dimensione. Gli aggiornamenti di una dimensione abilitata per la scrittura vengono registrati direttamente nella tabella della dimensione. Questa funzionalità avanzata modifica l'impostazione della proprietà **WriteEnabled** per una dimensione.  
  
 Per aggiungere il writeback della dimensione, usare Configurazione guidata funzionalità di Business Intelligence e selezionare l'opzione **Abilitazione writeback della dimensione** nella pagina **Scelta funzionalità avanzata** . Questa procedura guidata consente di eseguire in modo semplificato i passaggi per la selezione di una dimensione alla quale si desidera applicare il writeback della dimensione e per l'impostazione di questa opzione per la dimensione selezionata.  
  
> [!NOTE]  
>  Il writeback è supportato solo per i database relazionali e i data mart di SQL Server.  
  
## <a name="selecting-a-dimension"></a>Selezione di una dimensione  
 Nella prima pagina della procedura guidata **Abilitazione writeback della dimensione** specificare la dimensione alla quale si desidera applicare il writeback della dimensione. La funzionalità avanzata di writeback della dimensione aggiunta alla dimensione selezionata risulterà tra le modifiche apportate alla dimensione. Tali modifiche verranno ereditate da tutti i cubi che includono la dimensione selezionata.  
  
## <a name="setting-dimension-writeback-capability"></a>Impostazione della funzionalità di writeback della dimensione  
 Nella seconda pagina della procedura guidata **Abilitazione writeback della dimensione** è possibile effettivamente impostare l'opzione **Consenti writeback della dimensione** . Selezionando questa opzione, la proprietà **WriteEnabled** della dimensione viene impostata automaticamente su **True**. Deselezionando questa opzione la proprietà viene impostata automaticamente su **False**.  
  
## <a name="remarks"></a>Note  
 Quando si crea un nuovo membro, è necessario includere ogni attributo di una dimensione. Non è possibile inserire un membro senza specificare un valore per l'attributo chiave della dimensione. La creazione di membri è pertanto soggetta a tutti i vincoli, ad esempio valori di chiave non Null, definiti nella tabella della dimensione. È consigliabile inoltre considerare le colonne che possono essere specificate dalle proprietà della dimensione, ad esempio quelle specificate nella proprietà della dimensione **CustomRollupColumn**, **CustomRollupPropertiesColumn** o **UnaryOperatorColumn** .  
  
> [!WARNING]  
>  Se si utilizza SQL Azure come origine dati per eseguire il writeback in un database di Analysis Services, l'operazione non viene completata. Questo si verifica per motivi strutturali, dal momento che l'opzione provider che abilita il servizio MARS (Multiple Active Result Sets) non è abilitata per impostazione predefinita.  
>   
>  La soluzione alternativa consiste nell'aggiungere l'impostazione seguente nella stringa di connessione, per supportare il servizio MARS e abilitare il writeback:  
>   
>  `"MultipleActiveResultSets=True"`  
>   
>  Per altre informazioni vedere [Utilizzo di MARS &#40;Multiple Active Result Set&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Dimensioni abilitate per la scrittura](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
