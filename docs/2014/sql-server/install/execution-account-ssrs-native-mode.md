---
title: Account di esecuzione (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.executionaccount.F1
ms.assetid: 440b5a09-5fd4-4c3a-b510-f3c33cbf1c82
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0eff6dca788744b93d2d6d4a0a7175764e263f71
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952542"
---
# <a name="execution-account-ssrs-native-mode"></a>Account di esecuzione (modalità nativa SSRS)
  Utilizzare questa pagina per configurare un account da utilizzare per l'esecuzione automatica. L'account verrà utilizzato in circostanze particolari, ovvero quando non sono disponibili altre origini di credenziali, in particolare:  
  
-   Quando il server di report si connette a un'origine dei dati per cui non sono necessarie credenziali. Tra gli esempi di origini dati che potrebbero non necessitare di credenziali rientrano i documenti XML e alcune applicazioni di database client.  
  
-   Quando il server di report si connette a un altro server per recuperare file di immagine esterni o altre risorse a cui si fa riferimento in un report.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità nativa.  
  
 L'impostazione di questo account è facoltativa, tuttavia se non viene eseguita viene limitato l'utilizzo di immagini e connessioni esterne ad alcune origini dati. Quando si recuperano immagini di file esterni, il server di report verifica se è possibile eseguire una connessione anonima. Se la connessione è protetta da password, il server di report utilizza l'account per l'esecuzione automatica dei report per connettersi al server remoto. Durante il recupero di dati per un report, il server di report rappresenta l'utente corrente, richiede all'utente di specificare le credenziali, utilizza le credenziali archiviate oppure utilizza l'account per l'esecuzione automatica se la connessione all'origine dati non specifica **alcun** tipo di credenziale. Il server di report non consente la delega o la rappresentazione delle credenziali dell'account di servizio quando ci si connette ad altri computer, pertanto è necessario utilizzare l'account per l'esecuzione automatica se non sono disponibili altre credenziali.  
  
 L'account specificato deve essere diverso da quello utilizzato per l'esecuzione dell'account del servizio. In caso si configuri questo account, verrà archiviato nel file RSReportServer.config come valore crittografato. Se il server di report viene eseguito in una distribuzione con scalabilità orizzontale, è necessario configurare questo account allo stesso modo in ogni server di report.  
  
 È possibile utilizzare qualsiasi account utente di Windows. Per ottenere risultati ottimali, scegliere un account che disponga delle autorizzazioni di lettera e di accesso alla rete per supportare le connessioni ad altri computer. Deve disporre di autorizzazioni di lettura per qualsiasi immagine o file di dati esterno da utilizzare in un report. Non specificare un account locale se tutte le origini dati e tutte le immagini esterne per i report non sono archiviate sul computer del server di report. Utilizzare l'account solo per l'elaborazione automatica dei report.  
  
> [!NOTE]  
>  Se si utilizza [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] with Advanced Services, è necessario configurare questo account solo se si fa riferimento a immagini esterne in un report ed è necessaria l'autorizzazione per accedere al file di immagine. In SQL Server Express la connessione all'origine dati in un server remoto non è supportata. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473).  
  
 Per aprire questa pagina, avviare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e selezionare **Account di esecuzione** nel riquadro di navigazione. Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opzioni  
 **Specifica account di esecuzione**  
 Selezionare questa opzione per specificare un account.  
  
 **Account**  
 Immettere un account utente di dominio di Windows. Usare questo formato: * \<dominio>\\<account\>utente*.  
  
 **Password**  
 Digitare la password.  
  
 **Conferma password**  
 digitare nuovamente la password.  
  
## <a name="see-also"></a>Vedere anche  
 [Reporting Services Configuration Manager argomenti della Guida F1 &#40;modalità nativa di SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Archiviare i dati crittografati del server di report &#40;Gestione configurazione SSRS &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
  
  
