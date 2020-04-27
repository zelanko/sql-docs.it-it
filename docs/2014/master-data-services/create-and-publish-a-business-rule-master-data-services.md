---
title: Creare e pubblicare una regola business (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], creating
- creating business rules [Master Data Services]
ms.assetid: 6961d636-4d69-468e-81f7-8d0be6a4a039
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2b52be0b8c76333b069c018415ff698f13f824ae
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65479890"
---
# <a name="create-and-publish-a-business-rule-master-data-services"></a>Creare e pubblicare una regola business (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare una regola business per garantire l'accuratezza dei dati master. Dopo avere creato una regola, è necessario pubblicarla prima di poterla applicare ai dati.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-create-and-publish-a-business-rule"></a>Per creare e pubblicare una regola business  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Dalla barra dei menu scegliere **Gestisci** e fare clic su **Regole business**.  
  
3.  Nella pagina **Manutenzione regola business** selezionare un modello dall'elenco **Modello** .  
  
4.  Dall'elenco **Entità** selezionare un'entità.  
  
5.  Dall'elenco **Tipo di membro** selezionare un tipo di membro a cui applicare la regola di business.  
  
6.  Dall'elenco **Attributo** selezionare un attributo o lasciare inalterata l'impostazione predefinita **Tutti**.  
  
7.  Fare clic su **Aggiungi regola di business**.  
  
8.  Fare clic su **Modifica regola business selezionata**.  
  
9. Nel riquadro **Componenti** espandere il nodo **Condizioni** .  
  
10. Fare clic su una condizione e trascinarla nell'etichetta **condizioni** del riquadro **if** .  
  
    > [!TIP]  
    >  È possibile eliminare elementi dalla regola business facendo clic con il pulsante destro del mouse e scegliendo **Elimina**.  
  
11. Nel riquadro **attributi** fare clic su un attributo e trascinarlo sull'etichetta **Seleziona attributo** del riquadro **Modifica condizione** .  
  
12. Nel riquadro **Modifica condizione** completare tutti i campi obbligatori.  
  
13. Nel riquadro **Modifica condizione** fare clic su **Salva elemento**.  
  
14. Nel riquadro **Componenti** espandere il nodo **Azioni** .  
  
15. Fare clic su un'azione e trascinarla nell'etichetta **Azione** del riquadro **THEN** .  
  
16. Nel riquadro **Attributi** fare clic su un attributo e trascinarlo nell'etichetta **Seleziona attributo** del riquadro **Modifica azione** .  
  
17. Nel riquadro **Modifica azione** completare tutti i campi obbligatori.  
  
18. Nel riquadro **Modifica azione** fare clic su **Salva elemento**.  
  
19. Aggiungere facoltativamente più condizioni alla regola. Per altre informazioni, vedere [Aggiungere più condizioni a una regola business &#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md).  
  
20. Fare clic su **Indietro**.  
  
21. Facoltativamente, nella pagina **Manutenzione regola business** per la riga che contiene la regola business fare doppio clic su una cella nella colonna **Nome**, **Descrizione**o **Notifica** per aggiornare il valore.  
  
    > [!NOTE]  
    >  Le notifiche vengono inviate soltanto per le regole che prevedono un'azione di convalida.  
  
22. Fare clic su **Pubblica regole business**.  
  
23. Nella finestra di dialogo di conferma fare clic su **OK**. Lo stato della regola viene modificato in **Attiva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   Applicare regole business ai dati eseguendo una delle procedure riportate di seguito:  
  
    -   [Convalidare membri specifici rispetto a regole business &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Convalidare una versione usando le regole di business &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Configurare regole business per l'invio di notifiche &#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)   
 [Modificare il nome di una regola business &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Aggiungere più condizioni a una regola business &#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)  
  
  
