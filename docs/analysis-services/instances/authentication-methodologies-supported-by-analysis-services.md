---
title: Metodologie di autenticazione supportate da Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fe2c4021792c3285165440fc0627aa7eab374882
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62659220"
---
# <a name="authentication-methodologies-supported-by-analysis-services"></a>Metodologie di autenticazione supportate da Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Per la connessione a un'istanza di Analysis Services da un'applicazione client è necessaria l'autenticazione di Windows (integrata). È possibile fornire un'identità utente di Windows utilizzando uno dei metodi seguenti:  
  
-   NTLM  
  
-   Kerberos (vedere [Configurare Analysis Services per la delega vincolata Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md))  
  
-   EffectiveUserName nella stringa di connessione  
  
-   Accesso di base o anonimo (è necessaria la configurazione per l'accesso HTTP)  
  
-   Credenziali archiviate.  
  
 Si noti che l'autenticazione delle attestazioni non è supportata. Non è possibile utilizzare i token delle attestazioni di Windows per accedere ad Analysis Services. Le librerie client di Analysis Services supportano solo i principi di sicurezza di Windows. Se la soluzione di Business Intelligence include le identità delle attestazioni, sarà necessario disporre di account shadow di identità di Windows per ogni utente oppure utilizzare le credenziali archiviate per accedere ai dati di Analysis Services.  
  
 Per altre informazioni sui flussi di autenticazione di Analysis Services e Business Intelligence, vedere [Microsoft BI Authentication and Identity Delegation](http://go.microsoft.com/fwlink/?LinkID=286576)(Autenticazione di Microsoft Business Intelligence e la delega dell'identità).  
  
##  <a name="bkmk_auth"></a> Individuazione delle possibilità di autenticazione  
 Per la connessione a un database di Analysis Services è necessaria un'identità di gruppo o utente Windows e le relative autorizzazioni associate. L'identità può essere costituita da un account di accesso generico utilizzato da chiunque voglia visualizzare un report o, più probabilmente, dall'identità di singoli utenti.  
  
 In un modello tabulare o multidimensionale sono spesso presenti diversi livelli di accesso ai dati, per oggetto o all'interno dei dati stessi, in base all'autore della richiesta. Per soddisfare questo requisito, è possibile utilizzare NTLM, Kerberos, EffectiveUserName o l'autenticazione di base. Le tecniche sopra descritte permettono di passare identità utente diverse con ciascuna connessione. Tuttavia, la maggior parte di tali scelte è soggetta a una limitazione a un hop singolo. Soltanto nel caso di Kerberos con delega è possibile far passare l'identità utente originale tra più connessioni verso un archivio dati di back-end in un server remoto.  
  
 **NTLM**  
  
 Per connessioni che specificano `SSPI=Negotiate`, NTLM è il sottosistema di autenticazione di backup usato quando non è disponibile un controller di dominio Kerberos. Con NTLM qualsiasi applicazione client o utente è in grado di accedere a risorse del server, purché la richiesta sia una connessione diretta da un client al server, la persona che richiede la connessione sia autorizzata ad accedere alla risorsa e i computer client e server siano nello stesso dominio.  
  
 Nelle soluzioni multilivello, la restrizione a un hop singolo di NLTM può costituire un limite notevole. L'identità utente che esegue la richiesta può essere rappresentata in un solo server remoto e non oltre. Se l'operazione corrente richiede l'esecuzione di servizi in più computer, è necessario configurare la delega vincolata Kerberos per riutilizzare il token di sicurezza in un server back-end. In alternativa, è possibile utilizzare credenziali archiviate o l'autenticazione di base per passare nuove informazioni sull'identità per una connessione a hop singolo.  
  
 **Autenticazione Kerberos e delega vincolata Kerberos**  
  
 L'autenticazione Kerberos è alla base della sicurezza integrata di Windows nei domini Active Directory. Come per NTLM, in Kerberos la rappresentazione è limitata a un hop singolo a meno che la delega non sia abilitata.  
  
 Per il supporto delle connessioni multi-hop, in Kerberos sono disponibili sia deleghe vincolate che deleghe non vincolate. Nella maggior parte degli scenari, tuttavia, la delega vincolata è considerata una procedura di sicurezza consigliata. La delega vincolata consente al servizio di passare il token di sicurezza dell'identità utente a un servizio legacy designato in un computer remoto. Per applicazioni multilivello, un requisito comune è la delega di un'identità utente da un server applicazioni di livello intermedio a un database back-end quale Analysis Services. Ad esempio, un modello tabulare o multidimensionale che restituisce dati diversi in base all'identità utente richiedere la delega dell'identità da un servizio di livello intermedio per evitare che l'utente debba immettere nuovamente le credenziali o ottenere le credenziali di sicurezza in altro modo.  
  
 Per la delega vincolata è necessaria una configurazione aggiuntiva in Active Directory, in cui i servizi alle estremità di invio e di ricezione sono autorizzati in modo esplicito per la delega. Nonostante i costi iniziali di configurazione, una volta configurato il servizio gli aggiornamenti delle password sono gestiti in modo indipendente in Active Directory. Non è necessario aggiornare le informazioni sugli account archiviate nelle applicazioni, come invece sarebbe necessario utilizzando l'opzione relativa alle credenziali archiviate descritta più in là.  
  
 Per altre informazioni sulla configurazione di Analysis Services per la delega vincolata, vedere [Configurare Analysis Services per la delega vincolata Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
> [!NOTE]  
>  In Windows Server 2012 è supportata la delega vincolata tra i domini. Per la configurazione della delega vincolata Kerberos in domini con livelli funzionali inferiori, invece, quali Windows Server 2008 o 2008 R2, è necessario che sia il computer client che il server siano membri dello stesso dominio.  
  
 **EffectiveUserName**  
  
 EffectiveUserName è una proprietà della stringa di connessione utilizzata per passare informazioni sull'identità a Analysis Services. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint lo usa per registrare l'attività utente nei log dei dati di utilizzo. Excel Services e PerformancePoint Services possono utilizzarlo per recuperare dati utilizzati da cartelle di lavoro o dashboard in SharePoint. Può anche essere utilizzato in applicazioni o script personalizzati che eseguono operazioni su un'istanza di Analysis Services.  
  
 Per altre informazioni sull'uso di EffectiveUserName in SharePoint, vedere [Utilizzare EffectiveUserName di Analysis Services in SharePoint Server 2010](http://go.microsoft.com/fwlink/?LinkId=311905).  
  
 **Autenticazione di base e utente anonimo**  
  
 L'autenticazione di base è una quarta alternativa per la connessione a un server back-end come utente specifico. Con l'autenticazione di base, il nome utente e la password Windows vengono passati alla stringa di connessione e vengono introdotti ulteriori requisiti di crittografia in transito per garantire la protezione delle informazioni riservate durante il transito. Un vantaggio importante dell'autenticazione di base è che la richiesta di autenticazione può attraversare i limiti di dominio.  
  
 Per l'autenticazione anonima, è possibile impostare l'identità utente anonimo su un account utente di Windows specifico (IUSR_GUEST per impostazione predefinita) o su un'identità del pool di applicazioni. L'account utente anonimo verrà utilizzato per la connessione ad Analysis Services e deve disporre di autorizzazioni di accesso ai dati nell'istanza di Analysis Services. Con questo approccio, nella connessione viene utilizzata unicamente l'identità utente associata all'account anonimo. Se l'applicazione richiede una ulteriore gestione dell'identità, è necessario scegliere un altro approccio o fornire una ulteriore gestione dell'identità.  
  
 L'autenticazione di base e quella anonima sono disponibili solo quando si configura Analysis Services per l'accesso HTTP, utilizzando IIS e msmdpump.dll per stabilire la connessione. Per altre informazioni, vedere [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)(Autenticazione di Microsoft Business Intelligence e la delega dell'identità).  
  
 **Stored Credentials**  
  
 La maggior parte dei servizi dell'applicazione di livello intermedio include funzionalità di memorizzazione di nomi utente e password utilizzati successivamente per recuperare dati da un archivio dati legacy, ad esempio Analysis Services o il motore relazionale di SQL Server. Di conseguenza, le credenziali archiviate forniscono una ulteriore alternativa per il recupero dei dati. Tra i limiti di questo approccio vi sono l'overhead di manutenzione associato all'aggiornamento di nomi utente e password e l'utilizzo di una identità singola per la connessione. Se la soluzione in uso richiede l'identità del chiamante originale, le credenziali archiviate non sono la scelta giusta.  
  
 Per altre informazioni sulle credenziali archiviate, vedere [Creare, modificare ed eliminare origini dati condivise &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) e [Use Excel Services with Secure Store Service in SharePoint Server 2013](http://go.microsoft.com/fwlink/?LinkID=309869) (Utilizzare Excel Services con il servizio di archiviazione sicura in SharePoint Server 2013).  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo della rappresentazione con la sicurezza del trasporto](http://go.microsoft.com/fwlink/?LinkId=311727)   
 [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [Configurare Analysis Services per la delega vincolata Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Registrazione del nome SPN per un'istanza di Analysis Services](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)   
 [Connetti ad Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
