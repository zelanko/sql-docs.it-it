---
title: Archiviare dati crittografati del server di report (Gestione configurazione SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], encryption
- credentials [Reporting Services]
- cryptography [Reporting Services]
- confidential reports [Reporting Services]
- encryption [Reporting Services]
- databases [Reporting Services], encryption
ms.assetid: ac0f4d4d-fc4b-4c62-a693-b86e712e75f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8156e3d62e8aac027499ad1e267e1f6e14f5ef9a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108685"
---
# <a name="store-encrypted-report-server-data-ssrs-configuration-manager"></a>Archiviare i dati crittografati del server di report (Gestione configurazione SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] archivia i valori crittografati nel database del server di report e nei file di configurazione. La maggior parte dei valori crittografati è costituita da credenziali utilizzate per l'accesso a origini dei dati esterne dalle quali vengono recuperati i dati dei report. In questo argomento vengono descritti i valori crittografati, la funzionalità per la crittografia utilizzata in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e altri tipi di dati riservati archiviati di cui è importante essere a conoscenza.  
  
## <a name="encrypted-values"></a>Valori crittografati  
 Nell'elenco seguente vengono descritti i valori archiviati in un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Informazioni per la connessione e credenziali utilizzate da un server di report per la connessione a un database del server di report in cui sono archiviati dati interni del server.  
  
     Questi valori vengono specificati e crittografati nel corso dell'installazione o della configurazione del server di report. È possibile aggiornare le informazioni sulla connessione in qualsiasi momento usando lo strumento Configurazione di Reporting Services o l'utilità **rsconfig** . La crittografia delle impostazioni di configurazione viene eseguita utilizzando una chiave a livello di computer locale, che è disponibile per tutti gli utenti. Le informazioni per la connessione crittografate del server di report vengono archiviate nel file rsreportserver.config (nessun altro file di configurazione contiene impostazioni crittografate). Per altre informazioni, vedere [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
-   Credenziali archiviate utilizzate da un server di report per la connessione a origini dei dati esterne da cui vengono recuperati i dati di un report.  
  
     Questi valori vengono definiti quando si esegue la configurazione delle informazioni sulle origini dei dati per un report, quindi vengono archiviati come valori crittografati in un database del server di report. Il server di report utilizza una chiave simmetrica per crittografare e decrittografare questi dati. Per altre informazioni sulle credenziali archiviate, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../integration-services/connection-manager/data-sources.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Account di esecuzione automatica utilizzato dal server di report per la connessione ad altri computer al fine di recuperare file di immagine o dati esterni utilizzati in un report.  
  
     Questo account viene utilizzato quando è necessaria una connessione a un computer remoto e non sono disponibili altre credenziali per stabilire la connessione. Si tratta di un account utilizzato principalmente per supportare l'elaborazione automatica dei report senza l'utilizzo di credenziali per l'accesso all'origine dei dati. Se si creano report basati su origini dei dati che non richiedono né utilizzano credenziali per l'accesso ai dati, è necessario configurare questo account per il server di report da utilizzare.  
  
     In determinate circostanze questo account è obbligatorio e può essere creato solo tramite lo strumento Configurazione di Reporting Services o l'utilità **rsconfig**. Questo valore viene inoltre archiviato nel file rsreportserver.config. Questo account deve essere creato manualmente. Per altre informazioni su questo account e su come viene usato, vedere [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
-   La chiave simmetrica utilizzata per la crittografia.  
  
     Questo valore viene creato durante l'installazione o la configurazione del server, quindi viene archiviato come valore crittografato nel database del server di report. Il servizio Windows ReportServer utilizza questa chiave per crittografare e decrittografare i dati che sono archiviati nel database del server di report.  
  
## <a name="encryption-functionality-in-reporting-services"></a>Funzionalità per la crittografia in Reporting Services  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa funzioni di crittografia disponibili nel sistema operativo Windows. Sono supportate sia la crittografia simmetrica sia la crittografia asimmetrica.  
  
 I dati nel database del server di report vengono crittografati con una chiave simmetrica. È disponibile una sola chiave simmetrica per ogni database del server di report. La chiave simmetrica viene a sua volta crittografata utilizzando la chiave pubblica di una coppia di chiavi asimmetriche generata da Windows. La chiave privata viene mantenuta dall'account del servizio Windows ReportServer.  
  
 In una distribuzione del server di report con scalabilità orizzontale, in cui più istanze del server di report condividono lo stesso database del server di report, viene utilizzata una sola chiave simmetrica per tutti i nodi del server di report. Ogni nodo deve avere una copia della chiave simmetrica condivisa. Al momento della configurazione della distribuzione con scalabilità orizzontale viene automaticamente creata una copia della chiave simmetrica per ogni nodo. Ogni nodo crittografa quindi la propria copia della chiave simmetrica utilizzando la chiave pubblica di una coppia di chiavi specifica del relativo account del servizio Windows. Per altre informazioni su come viene creata la chiave simmetrica per le distribuzioni a istanza singola e con scalabilità orizzontale, vedere [Inizializzare un server di report &#40;Gestione configurazione SSRS&#41;](ssrs-encryption-keys-initialize-a-report-server.md).  
  
> [!NOTE]  
>  Quando si modifica l'account del servizio Windows ReportServer, le chiavi asimmetriche potrebbero cessare di essere valide, ostacolando le operazioni del server. Per evitare il problema utilizzare sempre lo strumento di configurazione Reporting Services per modificare le impostazioni dell'account di servizio. Quando si utilizza lo strumento di configurazione, le chiavi vengono automaticamente aggiornate. Per altre informazioni, vedere [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
## <a name="other-sources-of-confidential-data"></a>Altre origini di dati riservati  
 In un server di report sono archiviati altri dati non crittografati, che tuttavia possono contenere informazioni riservate che si desidera proteggere. In particolare, gli snapshot delle cronologie dei report e gli snapshot delle esecuzioni dei report contengono risultati di query che possono includere dati destinati solo a utenti autorizzati. Se si utilizzano snapshot per report che contengono dati riservati, è importante tenere presente che gli utenti in grado di aprire le tabelle di un database del server di report potrebbero visualizzare parti di report archiviati esaminando il contenuto della tabella.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non supporta la memorizzazione nella cache o la cronologia del report per i report che usano parametri basati sull'ID di sicurezza dell'utente.  
  
## <a name="see-also"></a>Vedi anche  
 [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
