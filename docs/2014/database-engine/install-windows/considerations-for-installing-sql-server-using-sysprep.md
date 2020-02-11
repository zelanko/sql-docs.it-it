---
title: Considerazioni sull'installazione di SQL Server tramite SysPrep | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: e1792eeb-2874-4653-b20e-3063f4eb4e5d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 201ccae98886e5126eb347c10d16985cbeeddffe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779136"
---
# <a name="considerations-for-installing-sql-server-using-sysprep"></a>Considerazioni sull'installazione di SQL Server tramite SysPrep
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep consente di preparare un'istanza autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un computer e di completare la configurazione in un secondo momento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep comporta un processo costituito da due passaggi per ottenere un'istanza autonoma configurata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I passaggi necessari sono i seguenti:  
  
-   [Preparare l'immagine](#BKMK_PrepareImage)  
  
     Tramite questo passaggio viene arrestato il processo di installazione dopo che sono stati installati i file binari del prodotto, senza configurare le informazioni specifiche del computer, della rete o dell'account per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in fase di preparazione.  
  
-   [Completare l'immagine](#BKMK_CompleteImage)  
  
     Questo passaggio consente di completare la configurazione di un'istanza predisposta di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Durante questo passaggio, è possibile fornire informazioni specifiche del computer, della rete e dell'account.  
  
 Per ulteriori informazioni sull'installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di tramite Sysprep, vedere [Install SQL Server 2014 using Sysprep](install-sql-server-using-sysprep.md).  
  
## <a name="common-uses-for-includessnoversionincludesssnoversion-mdmd-sysprep"></a>Utilizzi comuni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep  
 La funzionalità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep può essere utilizzata nei modi seguenti:  
  
-   Utilizzando il passaggio di preparazione dell'immagine, è possibile preparare una o più istanze non configurate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nello stesso computer. È possibile configurare queste istanze predisposte utilizzando il passaggio di completamento dell'immagine sullo stesso computer.  
  
-   È possibile acquisire il file di configurazione per l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dell'istanza predisposta e utilizzarlo per preparare ulteriori istanze non configurate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su più computer per una configurazione successiva.  
  
-   In combinazione con l'Utilità preparazione sistema di Windows (anche nota come Windows SysPrep), è possibile creare un'immagine del sistema operativo in cui sono incluse le istanze predisposte non configurate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul computer di origine. Successivamente è possibile distribuire l'immagine del sistema operativo a più computer. Dopo aver completato la configurazione del sistema operativo, è possibile configurare le istanze predisposte utilizzando il passaggio di completamento dell'immagine dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     L'Utilità preparazione sistema (SysPrep) di Windows viene utilizzata per preparare immagini del sistema operativo di Windows. Viene utilizzata per acquisire un'immagine personalizzata del sistema operativo per la distribuzione in un'organizzazione. Per ulteriori informazioni su SysPrep e sui relativi utilizzi, vedere [Che cos'è Sysprep](https://go.microsoft.com/fwlink/?LinkId=143546).  
  
## <a name="installation-media-considerations"></a>Considerazioni sul supporto di installazione  
 Se si utilizza una versione completa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], considerare gli elementi seguenti:  
  
-   Edizioni non Express di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   Per installare i file binari del prodotto, nel passaggio di preparazione dell'immagine viene utilizzata la copia di valutazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando l'istanza viene completata, l'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dipende dall'ID del prodotto fornito durante il passaggio di completamento dell'immagine.  
  
    -   Se si fornisce un ID del prodotto della copia di valutazione, il periodo di valutazione scadrà 180 giorni dopo il completamento dell'istanza predisposta.  
  
-   Edizioni Express di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   Per preparare un'istanza delle edizioni Express di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilizzare il supporto di installazione di Express.  
  
    -   Non è possibile specificare gli ID del prodotto per un'istanza predisposta delle edizioni Express di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="supported-includessnoversionincludesssnoversion-mdmd-installations"></a>Installazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportate  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , SysPrep supporta tutte le funzionalità, inclusi gli strumenti, di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 È possibile preparare più istanze per installazioni side-by-side di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o versioni precedenti. Le funzionalità di queste istanze devono supportare SysPrep.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client viene installato e completato automaticamente alla fine del passaggio di preparazione dell'immagine.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vengono preparati automaticamente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Vengono completati quando si completa l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite il passaggio di completamento dell'immagine.  
  
 Per informazioni sulle edizioni supportate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 È possibile eseguire un aggiornamento dell'edizione durante la configurazione di un'istanza predisposta di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa opzione non è supportata per le edizioni Express di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A partire da [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep supporta le installazioni del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dalla riga di comando.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-sysprep-limitations"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep  
 Il ripristino di un'istanza predisposta non è supportato. Se l'installazione non viene completata durante la preparazione o il completamento dell'immagine, è necessario eseguire la disinstallazione.  
  
##  <a name="BKMK_PrepareImage"></a> Preparare l'immagine  
 Tramite il passaggio relativo alla preparazione dell'immagine vengono installati il prodotto e le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ma non viene configurata l'installazione.  
  
 Le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da installare e il percorso di installazione per i file di installazione del prodotto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere specificati durante questo passaggio. È possibile preparare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite **Preparazione immagine di un'istanza autonoma di SQL Server** nella pagina **Avanzate** di **Centro installazione** o dal prompt dei comandi.  
  
-   È possibile preparare più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sullo stesso computer che possono essere completate in un secondo momento.  
  
-   È possibile aggiungere o rimuovere funzionalità supportate per le installazioni di SysPrep dalle istanze predisposte esistenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Al termine della preparazione dell'istanza, nel menu **Start** viene reso disponibile un collegamento per completare la configurazione dell'istanza predisposta di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="BKMK_CompleteImage"></a> Completare l'immagine  
 È possibile completare le istanze predisposte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite uno dei metodi seguenti:  
  
-   Utilizzare il collegamento nel menu Start.  
  
-   Accedere al passaggio **Completamento immagine di un'istanza autonoma predisposta** nella pagina **Avanzate** di **Centro installazione**.  
  
## <a name="see-also"></a>Vedere anche  
 [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)  
  
  
