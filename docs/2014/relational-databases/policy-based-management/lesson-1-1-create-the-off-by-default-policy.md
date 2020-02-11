---
title: Creare criteri Disattivata per impostazione predefinita | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 98fde3c5-297c-4d95-981e-95700bbf5ccd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c96443d7f46dee539fd7d39a91a168b3ed5a0d8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67792931"
---
# <a name="create-the-off-by-default-policy"></a>Creazione di criteri Disattivata per impostazione predefinita
  Questa attività consente di creare una condizione denominata Posta disattivata basata sul facet Configurazione superficie di attacco e di creare quindi un criterio denominato Disattivata per impostazione predefinita.  
  
### <a name="to-create-the-mail-off-condition"></a>Per creare la condizione Posta disattivata  
  
1.  In Esplora oggetti espandere **Gestione**, **Gestione criteri**e **Facet**, fare clic con il pulsante destro del mouse su **Configurazione superficie di attacco**, quindi scegliere **Nuova condizione**.  
  
2.  Nella finestra di dialogo **Crea nuova condizione** digitare **Posta disattivata** nella casella **Nome**.  
  
3.  Nella casella **Facet** verificare che il facet **Configurazione superficie di attacco** sia selezionato.  
  
4.  Nella casella **Campo** dell'area **Espressione** selezionare **\@DatabaseMailEnabled**, nella casella **Operatore selezionare** **=** e in **Valore** selezionare **False**.  
  
5.  Nella pagina **Descrizione** digitare una descrizione per la condizione, quindi scegliere **OK** per creare la condizione.  
  
### <a name="to-create-the-off-by-default-policy"></a>Per creare i criteri Disattivata per impostazione predefinita  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su **Configurazione superficie di attacco**, quindi scegliere **Nuovi criteri**.  
  
2.  Nella finestra di dialogo **Crea nuovi criteri** digitare **Disattivata per impostazione predefinita** nella casella **Nome**.  
  
3.  Lasciare deselezionata la casella di controllo **Abilitato** . La casella di controllo **Abilitato** si applica ai criteri automatizzati e questi criteri verranno eseguiti su richiesta.  
  
4.  Nella casella di controllo **Condizioni di controllo** scorrere verso il basso fino all'area **Configurazione superficie di attacco** , quindi selezionare **Posta disattivata** come condizione da controllare.  
  
5.  La casella **In base alle destinazioni** sarà vuota perché si tratta di criteri con ambito server.  
  
6.  Nella casella di controllo **Modalità di valutazione** selezionare **Su richiesta** come modalità di valutazione.  
  
7.  Nella casella di controllo **Restrizione server** selezionare **Nessuna**.  
  
8.  Nella pagina **Descrizione** digitare una descrizione dei criteri.  
  
9. È possibile specificare un collegamento ipertestuale a una pagina Web per i criteri nell'area **Collegamento ipertestuale alla Guida aggiuntiva** . Nella casella **Testo da visualizzare** digitare il testo che verrà visualizzato per il collegamento ipertestuale.  
  
10. Nella casella **Indirizzo** digitare un collegamento ipertestuale a una pagina della Guida, ad esempio la home page per il reparto IT della società.  
  
11. Per verificare l'indirizzo aprendo la pagina Web, fare clic su **Prova collegamento**.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Configurazione di un server per l'esecuzione di criteri Disattivata per impostazione predefinita](lesson-1-2-configure-a-server-to-run-the-off-by-default-policy.md)  
  
  
