---
title: Inizializzare un server di report (Gestione configurazione SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], initializing
- initialization process [Reporting Services]
- checking report server initializations
- scale-out deployments [Reporting Services]
- initializing report servers [Reporting Services]
- verifying report server initializations
ms.assetid: 861d4ec4-1085-412c-9a82-68869a77bd55
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f9bcb5e7818c4125b81d715d7e74f120a07449d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108743"
---
# <a name="initialize-a-report-server-ssrs-configuration-manager"></a>Inizializzare un server di report (Gestione configurazione SSRS)
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]un server inizializzato è un server in grado di crittografare e decrittografare dati in un database del server di report. L'inizializzazione è un requisito per il funzionamento del server di report. L'inizializzazione viene eseguita al primo avvio del servizio del server di report, quando il server di report viene unito in join alla distribuzione esistente o quando vengono ricreate manualmente le chiavi come parte del processo di recupero. Per altre informazioni su come e perché usare le chiavi di crittografia, vedere [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](ssrs-encryption-keys-manage-encryption-keys.md) e [Archiviare i dati crittografati del server di report &#40;Gestione configurazione SSRS&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md).  
  
 Le chiavi di crittografia sono basate in parte sulle informazioni sul profilo del servizio del server di report. Se si modifica l'identità utente utilizzata per l'esecuzione del servizio del server di report, è necessario aggiornare le chiavi di conseguenza. Se si utilizza lo strumento di configurazione di Reporting Services per modificare l'identità utente, questa operazione viene eseguita automaticamente.  
  
 Se per un qualche motivo l'inizializzazione ha esito negativo, il server di report restituisce un errore `RSReportServerNotActivated` in risposta alle richieste dell'utente e di servizio. In questo caso, potrebbe essere necessario risolvere i problemi di configurazione del sistema o del server. Per altre informazioni, vedere [SSRS: Troubleshoot Issues and Errors with Reporting Services](https://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) (SSRS: risoluzione di problemi ed errori di Reporting Services) (https://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) in Wiki di TechNet.  
  
## <a name="overview-of-the-initialization-process"></a>Panoramica del processo di inizializzazione  
 Il processo di inizializzazione crea e archivia una chiave simmetrica utilizzata per la crittografia. La chiave simmetrica viene creata dai servizi di crittografia di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e quindi utilizzata dal servizio del server di report per crittografare e decrittografare i dati. La chiave simmetrica è anch'essa crittografata con una chiave asimmetrica.  
  
 Nelle istruzioni seguenti viene descritto il processo di inizializzazione:  
  
1.  All'avvio iniziale, il servizio del server di report legge il file RSReportServer.config per ottenere l'identificatore dell'installazione e le informazioni di connessione al database.  
  
2.  Il servizio del server di report richiede una chiave pubblica ai servizi di crittografia. Windows crea una chiave privata e una chiave pubblica e invia la chiave pubblica al servizio del server di report.  
  
3.  Il servizio del server di report si connette al database del server di report e archivia i valori dell'identificatore dell'installazione e della chiave pubblica.  
  
4.  Il servizio del server di report chiama nuovamente i servizi di crittografia, questa volta per richiedere una chiave simmetrica. Windows crea la chiave simmetrica.  
  
5.  Il servizio del server di report si connette nuovamente al database del server di report e aggiunge la chiave simmetrica ai valori dell'identificatore dell'installazione e della chiave pubblica archiviati al passaggio 3. Prima di archiviarla, il servizio del server di report utilizza la chiave pubblica per crittografare la chiave simmetrica. Dopo che la chiave simmetrica è stata archiviata, il server di report viene considerato inizializzato e può essere utilizzato.  
  
## <a name="initializing-a-report-server-for-scale-out-deployment"></a>Inizializzazione di un server di report per la distribuzione con scalabilità orizzontale  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supporta un modello di distribuzione con scalabilità orizzontale che condivide un singolo database del server di report tra più istanze del server di report. Per unire in join una distribuzione con scalabilità orizzontale, è necessario che un server di report crei e archivi la propria copia della chiave simmetrica nel database condiviso. Sebbene i server che utilizzano il database utilizzino una sola chiave simmetrica, ogni server di report ha una propria copia della chiave. Le copie sono diversificate dal fatto che vengono crittografate in modo univoco tramite la chiave pubblica del rispettivo proprietario.  
  
 I primi passaggi del processo di inizializzazione di un server di report per la distribuzione con scalabilità orizzontale sono identici ai primi tre passaggi in cui viene descritta l'inizializzazione di una singola combinazione di server e database.  
  
 La differenza del processo di inizializzazione per una distribuzione con scalabilità orizzontale consiste nel modo in cui il server di report ottiene la chiave simmetrica. Quando il primo server viene inizializzato, ottiene la chiave simmetrica da Windows. Quando il secondo server viene inizializzato durante la configurazione per la distribuzione con scalabilità orizzontale, ottiene la chiave simmetrica dal servizio del server di report già inizializzato. La prima istanza del server di report utilizza la chiave pubblica della seconda istanza per creare una copia crittografata della chiave simmetrica per la seconda istanza del server di report. La chiave simmetrica non viene mai esposta come solo testo in nessuna fase di questo processo.  
  
## <a name="how-to-initialize-a-report-server"></a>Come inizializzare un server di report  
  
-   Per inizializzare un server di report, utilizzare lo strumento di configurazione di Reporting Services. L'inizializzazione viene eseguita automaticamente al momento della creazione e della configurazione del database del server di report. Per altre informazioni, vedere [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
-   Per inizializzare un server di report per la distribuzione con scalabilità orizzontale, è possibile usare la pagina Inizializzazione dello strumento Configurazione di Reporting Services oppure l'utilità **RSKeymgmt** . Per istruzioni dettagliate, vedere [Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](configure-a-native-mode-report-server-scale-out-deployment.md).  
  
> [!NOTE]  
>  **RSKeymgmt** è un'applicazione console che può essere eseguita da una riga di comando in un computer che ospita un'istanza del server di report che fa già parte di una distribuzione con scalabilità orizzontale. Quando viene eseguita l'utilità, vengono specificati gli argomenti per selezionare un'istanza remota del server di report che si desidera inizializzare.  
  
 Il server di report viene inizializzato solo se esiste una corrispondenza tra l'identificatore dell'installazione e la chiave pubblica. Se la corrispondenza esiste, viene creata una chiave simmetrica che rende possibile la crittografia reversibile. Se la corrispondenza non esiste, il server di report viene disabilitato e potrebbe essere necessario applicare una chiave di backup o eliminare i dati crittografati nel caso in cui la copia di backup non sia disponibile o non sia valida. Per altre informazioni sulle chiavi di crittografia usate da un server di report, vedere [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](ssrs-encryption-keys-manage-encryption-keys.md).  
  
> [!NOTE]  
>  È inoltre possibile utilizzare il provider Strumentazione gestione Windows (WMI) di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per inizializzare un server di report a livello di programmazione. Per altre informazioni, vedere [Accedere al provider WMI per Reporting Services](../tools/access-the-reporting-services-wmi-provider.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="how-to-confirm-a-report-server-initialization"></a>Come confermare l'inizializzazione di un server di report  
 Per confermare l'inizializzazione di un server di report, eseguire il ping del servizio Web ReportServer digitando **http://\<nomeserver>/reportserver** nella finestra di comando. Se si verifica l'errore `RSReportServerNotActivated`, l'inizializzazione non è riuscita.  
  
## <a name="see-also"></a>Vedere anche  
 [Archiviare i dati crittografati del server di report &#40;Gestione configurazione SSRS &#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
