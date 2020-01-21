---
title: 'Lezione 1: Creare e applicare criteri Disattivata per impostazione predefinita'
description: Esercitazione che spiega come creare e applicare i criteri Disattivata per impostazione predefinita per la gestione basata su criteri in SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d31367db-b7db-44c4-8df2-f1240474cf78
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1bff30a7270be7b47e5bf718d07d5386951042f1
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558006"
---
# <a name="lesson-1-create-and-apply-an-off-by-default-policy"></a>Lezione 1: Creare e applicare criteri Disattivata per impostazione predefinita
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Tramite i criteri della gestione basata su criteri è possibile amministrare una o più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uno o più oggetti dell'istanza, una o più istanze del server, uno o più database o uno o più oggetti di database. Gli amministratori del database desiderano impedire che in determinati server sia abilitato Posta elettronica database. In questa lezione verranno creati una condizione e i criteri per l'impostazione dell'opzione server in questione. Il server verrà quindi testato per verificarne la conformità ai criteri. Si utilizzeranno infine i criteri per riconfigurare il server per renderlo conforme.  

## <a name="prerequisites"></a>Prerequisites
Per completare questa esercitazione, sono necessari SQL Server Management Studio e l'accesso a un server che esegue SQL Server. 

- Installare [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Installare [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
  
## <a name="create-the-mail-off-condition"></a>Creare la condizione Posta disattivata

1.  In Esplora oggetti espandere **Gestione**, **Gestione criteri**e **Facet**, fare clic con il pulsante destro del mouse su **Configurazione superficie di attacco**, quindi scegliere **Nuova condizione**.  

    ![Nuova condizione](Media/lesson-1-create-and-apply-an-off-by-default-policy/new-surface-area-condition.png)
  
2.  Nella finestra di dialogo **Crea nuova condizione** digitare **Posta disattivata** nella casella **Nome**.   
    1. Nella casella **Facet** verificare che il facet **Configurazione superficie di attacco** sia selezionato.
    1. Nella casella **Campo** dell'area **Espressione** selezionare **\@DatabaseMailEnabled**, nella casella **Operatore selezionare** **=** e in **Valore** selezionare **False**.  
    1. Nella pagina **Descrizione** digitare una descrizione per la condizione, quindi scegliere **OK** per creare la condizione.  

    ![Condizione Posta disattivata](Media/lesson-1-create-and-apply-an-off-by-default-policy/mail-off-condition.png) 
  
## <a name="create-the-off-by-default-policy"></a>Creare i criteri Disattivata per impostazione predefinita  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su **Configurazione superficie di attacco**, quindi scegliere **Nuovi criteri**.  
  
2.  Nella finestra di dialogo **Crea nuovi criteri** digitare **Disattivata per impostazione predefinita** nella casella **Nome**. 
    1. Lasciare deselezionata la casella di controllo **Abilitato** . La casella di controllo **Abilitato** si applica ai criteri automatizzati e questi criteri verranno eseguiti su richiesta.
    1. Nella casella di controllo **Condizioni di controllo** scorrere verso il basso fino all'area **Configurazione superficie di attacco** , quindi selezionare **Posta disattivata** come condizione da controllare.
    1. La casella **In base alle destinazioni** sarà vuota perché si tratta di criteri con ambito server. 
    1. Nella casella di controllo **Modalità di valutazione** selezionare **Su richiesta** come modalità di valutazione.
    1. Nella casella di controllo **Restrizione server** selezionare **Nessuna**.
    1. Nella pagina **Descrizione** digitare una descrizione dei criteri.  

    ![Criteri Disattivata per impostazione predefinita](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy.png)
  
9. Nella pagina della descrizione è possibile specificare un collegamento ipertestuale a una pagina Web per i criteri nell'area **Collegamento ipertestuale alla Guida aggiuntiva**. Nella casella **Testo da visualizzare** digitare il testo che verrà visualizzato per il collegamento ipertestuale.
    1. Nella casella **Indirizzo** digitare un collegamento ipertestuale a una pagina della Guida, ad esempio la home page per il reparto IT della società.
    1. Per verificare l'indirizzo aprendo la pagina Web, fare clic su **Prova collegamento**.
    1. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

    ![Collegamento Web ai criteri Disattivata per impostazione predefinita](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy-web-link.png)


## <a name="configure-server-to-run-off-by-default-policy"></a>Configurare il server per l'esecuzione di criteri Disattivata per impostazione predefinita 

1.  In Esplora oggetti fare clic con il pulsante destro del mouse sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], scegliere **Criteri**e fare clic su **Valuta**.  

    ![valutare i criteri](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-policy.png)
  
2.  Nella finestra di dialogo **Valuta criteri[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile selezionare criteri da un'altra istanza di**  o da un file. Per questo passaggio, lasciare l'opzione **Origine[!INCLUDE[ssDE](../../includes/ssde-md.md)] impostata sull'istanza del** .  
    1. Nella sezione **Criteri** selezionare i criteri **Off By Default** (Disattivata per impostazione predefinita).
    1. Per determinare se il server è conforme ai criteri, fare clic su **Valuta**.
    1. Nell'area **Risultati[!INCLUDE[ssDE](../../includes/ssde-md.md)] verrà visualizzato un cerchio verde con un segno di spunta se il**  è conforme ai criteri. Verrà visualizzato un cerchio rosso con una X se il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non è conforme ai criteri. 

   ![Valutare i criteri Disattivata per impostazione predefinita](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-off-by-default-policy.png)

  
6.  Se si verifica un errore, nell'area **Dettagli di destinazione** verranno visualizzate informazioni aggiuntive nella colonna **Messaggio** . Nella colonna **Messaggio** fare clic su **Visualizza** per visualizzare un report contenente i risultati della verifica per ogni proprietà facet controllata. 

    ![Visualizzare i risultati della valutazione dei criteri](Media/lesson-1-create-and-apply-an-off-by-default-policy/view-results-of-policy-evaluation.png)
  
7.  La descrizione dei criteri viene visualizzata nella parte inferiore della pagina. Nella sezione **Guida aggiuntiva** è incluso il collegamento ipertestuale configurato per i criteri. Fare clic sul collegamento ipertestuale del messaggio per aprire la pagina Web specificata quando sono stati creat i criteri.   

1.  Chiudere il browser e la finestra di dialogo **Visualizzazione dettagliata risultati** .  

1. Se il server non è conforme e si vuole disabilitare Posta elettronica database, fare clic su **Applica** nella pagina **Risultati valutazione** .  
  
10. Chiudere le due finestre di dialogo **Visualizzazione dettagliata risultati** e **Valuta criteri** .   

   
## <a name="next-lesson"></a>Lezione successiva  
[Lezione 2: Creare e applicare criteri per gli standard di denominazione](../../relational-databases/policy-based-management/lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
  
