---
title: Aggiungere e rimuovere le chiavi di crittografia per una distribuzione con scalabilità orizzontale (Gestione configurazione SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- encryption keys [Reporting Services]
- deleting encryption keys
- removing encryption keys
- adding encryption keys
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 2da86fb3-4b4d-407f-9825-74dcc42486f5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 52ecac095d34882d8f65cdafaa83784aef86e2fc
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59967907"
---
# <a name="add-and-remove-encryption-keys-for-scale-out-deployment-ssrs-configuration-manager"></a>Aggiungere e rimuovere le chiavi di crittografia per una distribuzione con scalabilità orizzontale (Gestione configurazione SSRS)
  È possibile eseguire [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in una distribuzione con scalabilità orizzontale configurando più server di report per l'utilizzo di un database del server di report condiviso. L'appartenenza a una distribuzione con scalabilità orizzontale si basa sull'archiviazione o meno da parte del server di report di una chiave di crittografia nel database del server di report. Per controllare l'appartenenza alla distribuzione con scalabilità orizzontale, aggiungere e rimuovere chiavi di crittografia per istanze del server di report specifiche. La rimozione di nodi dalla distribuzione può essere eseguita in qualsiasi ordine. Per l'aggiunta di nodi a una distribuzione è necessario unire in join tutte le nuove istanze di un server di report che fa già parte della distribuzione.  
  
## <a name="using-the-reporting-services-configuration-tool-to-configure-scale-out-deployment"></a>Utilizzo dello strumento di configurazione di Reporting Services per configurare distribuzioni con scalabilità orizzontale  
 Il modo più semplice per configurare una distribuzione con scalabilità orizzontale consiste nell'utilizzare lo strumento di configurazione di Reporting Services. Per altre informazioni e istruzioni dettagliate, vedere [Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](configure-a-native-mode-report-server-scale-out-deployment.md).  
  
## <a name="using-rskeymgmt-to-configure-scale-out-deployment"></a>Utilizzo di Rskeymgmt per configurare una distribuzione con scalabilità orizzontale  
 Per inizializzare un'istanza del server di report affinché usi un database del server di report condiviso, eseguire l'utilità **rskeymgmt** . L'aggiunta di un server di report a una distribuzione con scalabilità orizzontale richiede l'inizializzazione del server di report. Per eseguire questa operazione sono necessarie le autorizzazioni di amministratore. È necessario disporre delle credenziali di amministratore per il computer remoto che ospita il server di report da unire in join alla distribuzione.  
  
#### <a name="how-to-join-a-report-server-to-a-scale-out-deployment-rskeymgmt"></a>Come unire in join un server di report a una distribuzione con scalabilità orizzontale (rskeymgmt)  
  
1.  Eseguire **rskeymgmt.exe** localmente nel computer che ospita un server di report già membro della distribuzione con scalabilità orizzontale.  
  
2.  Utilizzare l'argomento `-j` per unire in join un server di report al database del server di report. Utilizzare gli argomenti `-m` e `-n` per specificare l'istanza del server di report remoto che si desidera aggiungere alla distribuzione. Utilizzare gli argomenti `-u` e `-v` per specificare un account amministratore nel computer remoto. Se si sta creando una distribuzione con scalabilità orizzontale utilizzando più istanze del server di report sullo stesso computer, la sintassi da utilizzare è leggermente diversa. Per altre informazioni sulla sintassi da utilizzare, vedere [Utilità rskeymgmt &#40;SSRS&#41;](../tools/rskeymgmt-utility-ssrs.md).  
  
     Nell'esempio seguente vengono illustrati gli argomenti che è necessario specificare se si sta unendo in join un server di report remoto a una distribuzione con scalabilità orizzontale (è possibile omettere le credenziali se si dispone di autorizzazioni di amministratore sul computer remoto):  
  
    ```  
    rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
    ```  
  
#### <a name="how-to-remove-a-report-server-from-a-scale-out-deployment-rskeymgmt"></a>Come rimuovere un server di report da una distribuzione con scalabilità orizzontale (rskeymgmt)  
  
1.  Aprire il file rsreportserver.config del server di report che si desidera rimuovere e trovare l'ID di installazione. Per impostazione predefinita, il file si trova nel percorso Programmi\Microsoft SQL Server\MSSQL.*n*\Reporting Services\ReportServer).  
  
     Se è stata installata un'unica istanza, sul computer sarà presente un solo file rsreportserver.config. Se sono state installate più istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , utilizzare la pagina Stato server dello strumento di configurazione di Reporting Services per individuare l'identificatore dell'istanza, ad esempio MSSQL.2, per il server di report che si desidera rimuovere. Il nome della cartella in cui vengono archiviati i file di programma dell'istanza del server di report si baserà sull'identificativo istanza, ad esempio, Programmi\Microsoft SQL Server\MSSQL.2.  
  
2.  Eseguire **rskeymgmt.exe**. Questa utilità può essere eseguita in qualsiasi server di report appartenente a una distribuzione con scalabilità orizzontale.  
  
3.  Utilizzare l'argomento `-r` per rilasciare l'istanza del server di report dalla distribuzione con scalabilità orizzontale. Nell'esempio seguente vengono illustrati gli argomenti che è necessario specificare:  
  
    ```  
    rskeymgmt -r <installation ID>  
    ```  
  
 Questi passaggi rimuovono il server di report da una distribuzione con scalabilità orizzontale, ma non disinstallano l'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sul server di report. Dopo avere rimosso il server di report dalla distribuzione con scalabilità orizzontale, è possibile disinstallare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dal server, se su tale server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è più necessario. Per informazioni, vedere [Disinstallare un'istanza esistente di SQL Server &#40;programma di installazione&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](ssrs-encryption-keys-manage-encryption-keys.md)   
 [Inizializzare un server di report &#40;Gestione configurazione SSRS&#41;](ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
