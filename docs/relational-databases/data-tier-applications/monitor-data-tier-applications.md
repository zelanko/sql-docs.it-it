---
title: Monitorare le applicazioni livello dati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- monitoring [SQL Server], data-tier applications
- monitoring server performance [SQL Server], DACs
- data-tier application [SQL Server], monitor
ms.assetid: d2765828-2385-4019-aef2-1de3ab7d1b26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df8cd54cdf13941044ae4f72f8781e4532fc5c51
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588945"
---
# <a name="monitor-data-tier-applications"></a>Monitoraggio delle applicazioni livello dati
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un'applicazione livello dati (DAC) può essere monitorata da **Gestione Utilità** e **Esplora oggetti** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS), insieme alle viste e alle tabelle di sistema. Inoltre, tutti gli oggetti nel database contenuto in DAC possono essere monitorati utilizzando le tecniche di monitoraggio standard del database e del [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Se si distribuisce un'applicazione livello dati in un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)], le informazioni sul pacchetto di applicazione livello dati distribuito vengono incorporate in Utilità SQL Server al successivo invio del set di raccolta dell'utilità dall'istanza al punto di controllo dell'utilità. È quindi possibile visualizzare informazioni sull'integrità di base sull'Applicazione livello dati tramite [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Gestione Utilità**.  
  
 **Esplora oggetti** di SSMS consente di visualizzare informazioni di configurazione di base su ogni DAC distribuito in un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)], indipendentemente dal fatto che l'istanza sia gestita in Utilità SQL Server. Inoltre, il database associato a un DAC distribuito può essere monitorato mediante le stesse routine utilizzate per il monitoraggio di qualsiasi altro database.  
  
## <a name="using-the-sql-server-utility"></a>Utilizzo di Utilità SQL Server  
 La pagina dei dettagli **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) in **Esplora utilità** di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]visualizza un dashboard che segnala l'utilizzo delle risorse da parte di tutte le applicazioni livello dati che sono state distribuite a istanze di [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Nel riquadro superiore della pagina dei dettagli vengono elencati i DAC distribuiti con indicatori visivi che mostrano se il loro utilizzo delle risorse di CPU e file rientra tra i criteri definiti per Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Selezionando qualsiasi DAC nella visualizzazione Elenco, è possibile visualizzare ulteriori dettagli nelle schede nel riquadro inferiore della pagina. Per altre informazioni sulle informazioni presentate nella pagina dei dettagli, vedere [Dettagli di Applicazioni livello dati distribuite &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
 In seguito all'utilizzo della pagina dei dettagli **Applicazioni livello dati distribuite**, che consente di identificare rapidamente qualsiasi DAC che utilizzi troppo o troppo poco la risorsa hardware, è possibile pianificare la risoluzione di eventuali problemi. Più applicazioni del livello dati che non utilizzano completamente le risorse hardware potrebbero essere consolidate in un unico server, liberando così alcuni server per altri utilizzi. Se le risorse nel server corrente vengono utilizzate maniera eccessiva, è possibile spostare l'applicazione del livello dati in un server più grande o aggiungere altre risorse nel server corrente.  
  
 I limiti minimi e massimi per l'utilizzo delle risorse sono definiti dai criteri di monitoraggio delle applicazioni, definiti a loro volta nella pagina dei dettagli **Amministrazione utilità** . Gli amministratori del database possono personalizzare i criteri e far sì che rientrino nei limiti stabiliti dalle organizzazioni. Ad esempio, una società potrebbe impostare al 75% l'utilizzo massimo di CPU per un pacchetto DAC, mentre un'altra società potrebbe impostarlo all'80%. Per altre informazioni sull'impostazione dei criteri di monitoraggio delle applicazioni, vedere [Amministrazione utilità &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Per visualizzare la pagina dei dettagli **Applicazioni livello dati distribuite**:  
  
1.  Selezionare il menu **Visualizza/Esplora utilità** .  
  
2.  Connettere **Esplora utilità** al punto di controllo dell'utilità.  
  
3.  Selezionare il menu **Visualizza/Dettagli Esplora utilità** .  
  
4.  Selezionare il nodo **Applicazioni livello dati distribuite** in **Esplora utilità**.  
  
 Le informazioni contenute nella pagina dei dettagli **Applicazioni livello dati distribuite** provengono dai dati nel data warehouse di gestione dell'utilità, che per impostazione predefinita raccoglie i dati ogni 15 minuti. È possibile personalizzare l'intervallo utilizzando la pagina dei dettagli **Amministrazione utilità** .  
  
## <a name="using-object-explorer"></a>Utilizzo di Esplora oggetti  
 **Esplora oggetti** di SSMS consente di visualizzare informazioni di configurazione di base su ogni DAC distribuito in un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)], incluse le istanze che sono state registrate nell'utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le istanze autonome che non è possibile visualizzare in **Esplora utilità**.  
  
 Per visualizzare i dettagli di DAC distribuiti in un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]:  
  
1.  Selezionare il menu **Visualizza/Esplora oggetti** .  
  
2.  Connettersi all'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]dal riquadro Esplora oggetti.  
  
3.  Selezionare il menu **Visualizza/Dettagli Esplora oggetti** .  
  
4.  In **Esplora oggetti** selezionare il nodo del server che esegue il mapping nell'istanza, quindi passare al nodo **Gestione\Applicazioni livello dati** .  
  
5.  Nella visualizzazione Elenco nel riquadro superiore della pagina dei dettagli viene elencato ogni DAC distribuito nell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Selezionare DAC per visualizzare le informazioni nel riquadro dei dettagli in fondo alla pagina.  
  
 Il menu di scelta rapida del nodo **Applicazioni livello dati** è inoltre utilizzato per distribuire nuovi DAC o eliminare DAC esistenti.  
  
## <a name="using-the-dac-system-views-and-tables"></a>Utilizzo di viste e tabelle di sistema DAC  
 La tabella di sistema msdb.dbo.sysdac_history_internal consente di registrare l'esito positivo o negativo di tutte le azioni di gestione DAC eseguite in un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Nella tabella vengono registrati l'ora in cui si è verificata l'azione e l'account di accesso con cui questa è stata avviata. Per altre informazioni, vedere [sysdac_history_internal &#40;Transact-SQL&#41;](../../relational-databases/system-tables/data-tier-application-tables-sysdac-history-internal.md).  
  
 Nelle viste di sistema DAC vengono riportate le informazioni sul catalogo di base. Per altre informazioni, vedere [Viste applicazioni livello dati &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/0de01328-d7a6-4677-b7a0-dcd3098c23d4).  
  
## <a name="monitoring-dac-databases"></a>Monitoraggio dei database DAC  
 In seguito alla corretta distribuzione di DAC, il database contenuto in DAC funzionerà come qualsiasi altro database. Utilizzare le tecniche e gli strumenti standard del [!INCLUDE[ssDE](../../includes/ssde-md.md)] per il monitoraggio delle prestazioni, del log, degli eventi e dell'utilizzo delle risorse del database.  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Distribuire un'applicazione livello dati](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)  
  
  
