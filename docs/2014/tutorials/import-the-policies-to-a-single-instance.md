---
title: Importare i criteri in una singola istanza | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: bc5bcd87-663f-41d9-bb7b-b3e083cd63df
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 276d37b97cfe0a2a4194aa8aed713834a20c8674
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52522855"
---
# <a name="import-the-policies-to-a-single-instance"></a>Importazione dei criteri in un'istanza singola
  In questa attività verrà eseguita l'importazione dei criteri per procedure consigliate che si desidera pianificare nella gestione basata su criteri in una singola istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="prerequisites"></a>Prerequisiti  
 È necessario eseguire questa procedura in un server che esegue [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] o una versione successiva.  
  
### <a name="import-the-best-practices-policies-for-the-database-engine"></a>Importazione dei criteri per procedure consigliate per il Motore di database  
  
1.  Avviare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], quindi connettersi al [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  In Esplora oggetti, espandere **Management**, quindi espandere **gestione dei criteri**.  
  
3.  Fare doppio clic su **politiche**, quindi fare clic su **Importa criteri**.  
  
4.  Nel **importare** accanto alla finestra di dialogo il **i file da importare** fare clic sui puntini di sospensione (**...** ) pulsante.  
  
5.  Nel **Cerca in** elencare, esplorare la cartella seguente, che contiene i criteri per procedure consigliate migliori:  
  
     **C:\Programmi\Microsoft file (x86) \Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
    > [!NOTE]  
    >  Il percorso del file può variare in base alla posizione in cui sono stati installati i file di programma di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], all'esecuzione di un sistema operativo a 32 o a 64 bit e all'identificatore di lingua.  
  
6.  Nel **Seleziona criteri** nella finestra di dialogo, selezionare uno o più criteri file.  
  
     Per selezionare file non adiacenti, fare clic su un file, tenere premuto il tasto CTRL, quindi fare clic su ogni file aggiuntivo. Per selezionare file adiacenti, fare clic sul primo file nella sequenza, tenere premuto il tasto MAIUSC, quindi fare clic sull'ultimo file.  
  
7.  Dopo aver selezionato i file, fare clic **aperto**.  
  
8.  Nel **importare** finestra di dialogo, assicurarsi che le **lo stato dei criteri** elenco è impostato su **mantiene lo stato dei criteri al momento dell'importazione** (predefinito) e quindi fare clic su **OK**.  
  
     I criteri vengono importati nel **i criteri** nodo sotto **gestione dei criteri**. Per impostazione predefinita, i criteri importati sono impostati sulla modalità di valutazione "Su richiesta".  
  
## <a name="next-steps"></a>Passaggi successivi  
 [Pianificazione criteri](../../2014/tutorials/schedule-the-policies.md)  
  
  
