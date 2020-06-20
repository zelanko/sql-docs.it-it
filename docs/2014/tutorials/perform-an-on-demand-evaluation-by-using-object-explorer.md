---
title: Eseguire una valutazione su richiesta utilizzando Esplora oggetti | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: da56673e05c092c965554b76572ac3b0486d2110
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85044160"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>Esecuzione di una valutazione su richiesta utilizzando Esplora oggetti
  In questa attività verrà utilizzato Esplora oggetti per eseguire una valutazione su richiesta di criteri per procedure consigliate per il [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] in una singola istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  È inoltre possibile valutare criteri in un'istanza singola mediante Server registrati. Per ulteriori informazioni, vedere [eseguire una valutazione su richiesta tramite Server registrati](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questa lezione è basata sulla versione di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Per eseguire una valutazione su richiesta dei criteri per procedure consigliate per le istanze in cui è in esecuzione [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] , è necessario utilizzare la procedura descritta nell'argomento [eseguire una valutazione su richiesta tramite Server registrati](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>Per eseguire una valutazione su richiesta utilizzando Esplora oggetti  
  
1.  Avviare [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], quindi connettersi al [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  In Esplora oggetti espandere **gestione**, espandere **Gestione criteri**, fare clic con il pulsante destro del mouse su **criteri**, quindi scegliere **valuta**.  
  
    > [!NOTE]  
    >  Per impostazione predefinita, l'istanza locale viene utilizzata come origine dei criteri. Se in precedenza sono stati importati criteri per procedure consigliate, questi verranno elencati insieme agli altri criteri creati. È possibile selezionare uno dei criteri per procedure consigliate importati, quindi fare clic su **valuta**. Se non sono stati importati criteri per procedure consigliate, continuare con questa procedura.  
  
3.  Nella finestra di dialogo **Valuta criteri** , accanto alla casella **origine** , fare clic sul pulsante con i puntini di sospensione (**...**).  
  
4.  Nella finestra di dialogo **Seleziona origine** è possibile selezionare i **file** o il **server** come origine dei file di criteri da valutare. Se si fa clic su **Server**, è possibile eseguire una valutazione su richiesta dei criteri per procedure consigliate importati in precedenza nella gestione basata su criteri in un server locale o remoto. In questa esercitazione si fa clic su **file**, quindi si selezionano i singoli file dei criteri che si desidera valutare. A questo scopo, seguire questa procedura:  
  
    1.  Fare clic su **file**.  
  
    2.  Accanto a **file**fare clic sul pulsante con i puntini di sospensione (**...**).  
  
    3.  Nella finestra di dialogo **Seleziona criterio** individuare la cartella seguente, contenente i criteri per procedure consigliate:  
  
         **C:\Programmi (x86)\Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  Il percorso del file può variare in base alla posizione in cui sono stati installati i file di programma di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], all'esecuzione di un sistema operativo a 32 o a 64 bit e all'identificatore di lingua.  
  
    4.  Selezionare uno o più file di criteri con estensione XML da valutare, quindi fare clic su **Apri**.  
  
         L'elenco dei file selezionati viene visualizzato nella casella **file** .  
  
    5.  Nella finestra di dialogo **Seleziona origine** fare clic su **OK**.  
  
    6.  Se viene visualizzata la finestra di dialogo **caricamento dei criteri** , fare clic su **Chiudi**.  
  
     I criteri selezionati vengono elencati nella pagina di **selezione dei criteri** . L'icona di avviso accanto ai criteri indica che questi contengono script.  
  
5.  Fare clic su **valuta** per valutare i criteri.  
  
     Nella tabella dei **risultati** vengono elencati i risultati per ogni criterio. Un'icona "x" rossa indica che la conformità di criteri non è riuscita.  
  
6.  Per alcuni errori relativi ai criteri, la gestione basata su criteri consente di applicare immediatamente la conformità di criteri nella destinazione. Per questo tipo di errori verrà visualizzata una casella di controllo accanto ai criteri che presentano errori. Se si seleziona la casella di controllo, il pulsante **applica** diventa disponibile. Quando si fa clic su **applica**, l'impostazione non conforme verrà automaticamente aggiornata nell'istanza di di destinazione.  
  
    > [!CAUTION]  
    >  Assicurarsi di aver compreso a pieno tutte le impostazioni dei criteri prima di aggiornare automaticamente un'istanza di destinazione. Dopo aver selezionato una o più caselle di controllo, è consigliabile fare clic su **script**e scegliere un percorso di output in modo che sia possibile esaminare il [!INCLUDE[tsql](../includes/tsql-md.md)] codice sottostante prima di applicare le modifiche.  
  
7.  Per visualizzare i risultati dettagliati per un criterio, fare clic sul criterio nella tabella **dei risultati** .  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Esecuzione di una valutazione su richiesta utilizzando Server registrati](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
