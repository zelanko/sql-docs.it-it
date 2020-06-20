---
title: Inizializzare azioni basate su modifiche dei valori di attributo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], tracking attribute changes
- change tracking groups [Master Data Services], initiating actions
ms.assetid: 5e4402ce-31db-4774-a2a1-552335f87693
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4dffc314c99345c9e8db632fbcebc1f2e3653d2f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971361"
---
# <a name="initiate-actions-based-on-attribute-value-changes-master-data-services"></a>Inizializzare azioni basate su modifiche dei valori di attributo (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare una regola di business per inizializzare azioni in base alle modifiche dei valori di attributo. Ad esempio, quando un valore di attributo specifico viene modificato, è necessario modificare un valore, inviare una notifica o avviare un flusso di lavoro esterno.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Gli attributi devono essere in un gruppo rilevamento modifiche. Per altre informazioni, vedere [Aggiungere attributi ad un gruppo rilevamento modifiche &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md) .  
  
### <a name="to-create-a-business-rule-to-initiate-actions-based-on-attribute-value-changes"></a>Per creare una regola business per inizializzare azioni basate su modifiche dei valori di attributo  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Dalla barra dei menu scegliere **Gestisci** e fare clic su **Regole business**.  
  
3.  Nella pagina **Manutenzione regola business** selezionare un modello dall'elenco **Modello** .  
  
4.  Dall'elenco **Entità** selezionare un'entità.  
  
5.  Dall'elenco **Tipo di membro** selezionare un tipo di membro a cui applicare la regola di business.  
  
6.  Dall'elenco **Attributo** selezionare un attributo o lasciare inalterata l'impostazione predefinita **Tutti**.  
  
7.  Fare clic su **Aggiungi regola di business**.  
  
8.  Fare clic su **Modifica regola business selezionata**.  
  
9. Nel riquadro **Componenti** espandere il nodo **Condizioni** .  
  
10. Nel nodo **Confronto valori** trascinare **è stato modificato** nell'etichetta **Condizioni** del riquadro **IF** .  
  
11. Nel riquadro **attributi** fare clic su un attributo e trascinarlo sull'etichetta **Seleziona attributo** del riquadro **Modifica condizione** . Tale attributo non ha alcun effetto sulla regola, selezionare quindi qualsiasi attributo disponibile.  
  
12. Nel riquadro **Modifica condizione** nella casella **Gruppo rilevamento modifiche** digitare il numero del gruppo di rilevamento delle modifiche assegnato come parte dei prerequisiti.  
  
13. Nel riquadro **Modifica condizione** fare clic su **Salva elemento**.  
  
14. Nel riquadro **Componenti** espandere il nodo **Azioni** .  
  
15. Fare clic su un'azione e trascinarla nell'etichetta **Azione** del riquadro **THEN** .  
  
16. Nel riquadro **Attributi** fare clic su un attributo e trascinarlo nell'etichetta **Seleziona attributo** del riquadro **Modifica azione** .  
  
17. Nel riquadro **Modifica azione** completare tutti i campi obbligatori.  
  
18. Nel riquadro **Modifica azione** fare clic su **Salva elemento**.  
  
19. Fare clic su **Indietro**.  
  
20. Facoltativamente, nella pagina **Manutenzione regola business** per la riga che contiene la regola business fare doppio clic su una cella nella colonna **Nome**, **Descrizione**o **Notifica** per aggiornare il valore.  
  
    > [!NOTE]  
    >  Le notifiche vengono inviate soltanto per le regole che prevedono un'azione di convalida.  
  
21. Fare clic su **Pubblica regole business**.  
  
22. Nella finestra di dialogo di conferma fare clic su **OK**. Lo stato della regola viene modificato in **Attiva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   Applicare regole business ai dati eseguendo una delle procedure riportate di seguito:  
  
    -   [Convalidare membri specifici rispetto a regole business &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Convalidare una versione usando le regole di business &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere attributi a un gruppo di Rilevamento modifiche &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)   
 [Regole di business &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
