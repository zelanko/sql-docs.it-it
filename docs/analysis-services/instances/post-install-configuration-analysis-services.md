---
title: Configurazione (Analysis Services) successiva all'installazione | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aadcdb901c39af148b22640413b921aae288f016
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62711733"
---
# <a name="post-install-configuration-analysis-services"></a>Configurazione successiva all'installazione (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Dopo aver installato Analysis Services, è necessario eseguire ulteriori attività di configurazione per rendere il server completamente operativo e disponibile per l'utilizzo generale. In questa sezione vengono illustrate le attività aggiuntive per completare l'installazione. A seconda dei requisiti di connessione, potrebbe essere inoltre necessario configurare l'autenticazione (vedere [Connessione a un database di Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)).  
  
 In seguito saranno necessarie altre operazioni dopo aver preparato i database per la distribuzione. In particolare, sarà necessario configurare le appartenenze ai ruoli nel database per concedere l'accesso utente ai dati, progettare una strategia di backup e ripristino di un database e stabilire se è necessario un carico di lavoro di elaborazione pianificato per aggiornare i dati a intervalli regolari. Altre informazioni sulla distribuzione del database e l'amministrazione sono disponibili ai collegamenti seguenti: [I database modello multidimensionale](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md) e [i database modello tabulare](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md).  
  
## <a name="instance-configuration"></a>Configurazione dell'istanza  
 Analysis Services è un servizio replicabile, ovvero è possibile installare più istanze del servizio in un unico server. Ogni istanza aggiuntiva viene installata separatamente come istanza denominata, tramite il programma di installazione di SQL Server, e configurata in modo indipendente per supportare lo scopo desiderato. Ad esempio, un server di sviluppo può eseguire l'utilità Traccia eventi o utilizzare valori predefiniti per l'archiviazione dei dati che è possibile modificare altrimenti nei server che supportano i carichi di lavoro di produzione. Un altro esempio in cui è necessario modificare la configurazione di sistema è rappresentato dall'installazione dell'istanza di Analysis Services su hardware condiviso da altri servizi. Durante l'hosting di più applicazioni caratterizzate da un utilizzo elevato di dati nello stesso hardware, è possibile configurare le proprietà del server tramite cui vengono abbassate le soglie di memoria per ottimizzare le risorse disponibili in tutte le applicazioni.  
  
## <a name="post-installation-tasks"></a>Attività successive all'installazione  
  
|Collegamento|Descrizione dell'attività|  
|----------|----------------------|  
|[Configurare Windows Firewall per consentire l'accesso ad Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Creare una regola in ingresso in Windows Firewall per consentire il routing delle richieste tramite la porta TCP utilizzata dall'istanza di Analysis Services. Questa attività è obbligatoria. Nessuno può accedere ad Analysis Services da un computer remoto se non si definisce una regola firewall in ingresso.|  
|[Concedere i diritti di amministratore del server a un'istanza di Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)|Durante l'installazione è necessario aggiungere almeno un account utente al ruolo di amministratore dell'istanza di Analysis Services. Le autorizzazioni amministrative sono necessarie per molte operazioni di routine del server, ad esempio l'elaborazione di dati di database relazionali esterni. Utilizzare le informazioni contenute in questo argomento per aggiungere o modificare l'appartenenza al ruolo di amministratore.|
|[Configurare il software antivirus sui computer che eseguono SQL Server](https://support.microsoft.com/kb/309422) |Potrebbe essere necessario configurare software di scansione, ad esempio applicazioni antivirus e antispyware, per escludere le cartelle e i tipi di file di SQL Server. Se il software di scansione blocca un file di programma o dati quando Analysis Services ha bisogno di usarlo, può verificarsi un'interruzione del servizio o il danneggiamento dei dati. |
|[Configurare gli account del servizio &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)|Durante l'installazione è stato eseguito il provisioning dell'account del servizio Analysis Services con le autorizzazioni appropriate per consentire l'accesso controllato ai file eseguibili e di database. Come attività di post-installazione, a questo punto è necessario valutare se consentire l'utilizzo dell'account del servizio durante l'esecuzione di attività aggiuntive. I carichi di lavoro di query e di elaborazione possono essere eseguiti con l'account del servizio. Tali operazioni hanno esito positivo solo quando l'account del servizio dispone di autorizzazioni appropriate.|  
|[Registrare un'istanza di Analysis Services in un gruppo di server](../../analysis-services/instances/register-an-analysis-services-instance-in-a-server-group.md)|SQL Server Management Studio (SSMS) consente di creare gruppi di server per l'organizzazione delle istanze di SQL Server. Le distribuzioni scalabili costituite da più istanze server sono più semplici da gestire in gruppi di server. Utilizzare le informazioni contenute in questo argomento per organizzare le istanze di Analysis Services in gruppi in SSMS.|  
|[Determinare la modalità server di un'istanza di Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)|Durante l'installazione si sceglie una modalità server che determina il tipo di modello (multidimensionale o tabulare) in esecuzione nel server. Se non si è certi della modalità server, utilizzare le informazioni contenute in questo argomento per determinare la modalità installata.|  
|[Rinominare un'istanza di Analysis Services](../../analysis-services/instances/rename-an-analysis-services-instance.md)|Nomi descrittivi agevolano la distinzione tra più istanze con modalità server diverse o tra istanze utilizzate principalmente da determinati reparti o team dell'organizzazione. Utilizzare le informazioni contenute in questo argomento per apprendere come sostituire il nome di un'istanza con uno che semplifichi la gestione delle istallazioni.|  
  
## <a name="next-steps"></a>Passaggi successivi  
 Sono disponibili informazioni su come connettersi ad Analysis Services da applicazioni Microsoft o personalizzate mediante le librerie client. A seconda dei requisiti della soluzione, potrebbe essere inoltre necessario configurare il servizio per l'autenticazione Kerberos. Le connessioni che devono attraversare i limiti di dominio richiedono l'accesso HTTP. Per istruzioni sui passaggi successivi, vedere [Connect to Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione per SQL Server 2016](../../database-engine/install-windows/installation-for-sql-server-2016.md)   
 [Installazione di Analysis Services in modalità Multidimensionale e Data Mining](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [Installare Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)   
 [Installazione di Analisi Services in modalità Power Pivot](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  
