---
title: Importare i criteri in un'istanza singola | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: bc5bcd87-663f-41d9-bb7b-b3e083cd63df
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 83d688a72efaaf75305e5077634f70b016bad818
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039976"
---
# <a name="import-the-policies-to-a-single-instance"></a>Importazione dei criteri in un'istanza singola
  In questa attività verrà eseguita l'importazione dei criteri per procedure consigliate che si desidera pianificare nella gestione basata su criteri in una singola istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="prerequisites"></a>Prerequisiti  
 È necessario eseguire questa procedura in un server che esegue [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] o una versione successiva.  
  
### <a name="import-the-best-practices-policies-for-the-database-engine"></a>Importazione dei criteri per procedure consigliate per il Motore di database  
  
1.  Avviare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], quindi connettersi al [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  In Esplora oggetti espandere **gestione**, quindi **Gestione criteri**.  
  
3.  Fare clic con il pulsante destro del mouse su **criteri**, quindi scegliere **Importa criterio**.  
  
4.  Nella finestra di dialogo **Importa** fare clic sul pulsante con i puntini di sospensione (**..**.) accanto alla casella **file da importare** .  
  
5.  Nell'elenco **Cerca in** passare alla cartella seguente, che contiene i criteri per procedure consigliate:  
  
     **C:\Programmi (x86)\Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
    > [!NOTE]  
    >  Il percorso del file può variare in base alla posizione in cui sono stati installati i file di programma di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], all'esecuzione di un sistema operativo a 32 o a 64 bit e all'identificatore di lingua.  
  
6.  Nella finestra di dialogo **Seleziona criterio** selezionare uno o più file di criteri.  
  
     Per selezionare file non adiacenti, fare clic su un file, tenere premuto il tasto CTRL, quindi fare clic su ogni file aggiuntivo. Per selezionare file adiacenti, fare clic sul primo file nella sequenza, tenere premuto il tasto MAIUSC, quindi fare clic sull'ultimo file.  
  
7.  Al termine della selezione dei file, fare clic su **Apri**.  
  
8.  Nella finestra di dialogo **Importa** verificare che l'elenco **stato criteri** sia impostato **su Mantieni lo stato dei criteri durante l'importazione** (impostazione predefinita), quindi fare clic su **OK**.  
  
     I criteri vengono importati nel nodo **criteri** in **Gestione criteri**. Per impostazione predefinita, i criteri importati sono impostati sulla modalità di valutazione "Su richiesta".  
  
## <a name="next-steps"></a>Passaggi successivi  
 [Pianificazione criteri](../../2014/tutorials/schedule-the-policies.md)  
  
  
