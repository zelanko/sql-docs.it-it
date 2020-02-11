---
title: Distribuzione con scalabilità orizzontale (server di report in modalità nativa) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.scaleoutdeployment.F1
ms.assetid: 4df38294-6f9d-4b40-9f03-1f01c1f0700c
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a9fe82102df73ddfa77b4636dd29793ac2694949
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952422"
---
# <a name="scale-out-deployment-native-mode-report-server"></a>Distribuzione con scalabilità orizzontale (server di report in modalità nativa)
  La pagina **Distribuzione con scalabilità orizzontale** di Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] consente di visualizzare lo stato di inizializzazione per una distribuzione con scalabilità orizzontale o di creare un join di un server di report per una distribuzione con scalabilità orizzontale. Per *distribuzione con scalabilità orizzontale* si intendono due o più istanze del server di report che condividono un singolo database del server di report.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità nativa.  
  
 Per *server di report inizializzato* si intende un server in grado di crittografare e decrittografare dati riservati archiviati in un database del server di report. Le credenziali archiviate e le stringhe di connessione sono esempi di dati crittografati archiviati nel database. L'inizializzazione è un requisito necessario per il funzionamento del server di report.  
  
 La *distribuzione con scalabilità orizzontale* viene usata negli scenari seguenti:  
  
-   Come prerequisito per il bilanciamento del carico di più server di report in un cluster di server. Prima di bilanciare il carico di più server di report, è innanzitutto necessario configurare i server di report per la condivisione dello stesso database del server di report.  
  
-   Per segmentare applicazioni del server di report in computer diversi, utilizzando un server per l'elaborazione interattiva dei report e un secondo server per l'elaborazione pianificata dei report. In questo scenario ogni istanza del server elabora tipi diversi di richieste per lo stesso contenuto del server di report archiviato nel database del server di report condiviso.  
  
 Per configurare una distribuzione con scalabilità orizzontale, iniziare con una o più istanze del server di report tutte connesse allo stesso database del server di report. In seguito all'installazione di tutte le istanze, connettersi al primo server di report e quindi utilizzare la pagina Distribuzione con scalabilità orizzontale aggiungere ogni istanza aggiuntiva. Solo un server di report già inizializzato per l'utilizzo di un database può inizializzare nodi aggiuntivi.  
  
 Per aprire questa pagina, avviare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e selezionare **Distribuzione con scalabilità orizzontale** nel riquadro di navigazione. Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opzioni  
 **Nome server SQL**  
 Consente di specificare il nome [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] dell'istanza di che ospita il database del server di report.  
  
 **Nome database**  
 Consente di specificare il nome del database a cui è attualmente connessa l'istanza del server di report.  
  
 **Modalità server**  
 Consente di visualizzare la modalità del server e del database. La modalità del server è la modalità nativa o la modalità integrata SharePoint. Le distribuzioni con scalabilità orizzontale sono supportate per entrambe le modalità.  
  
 **Server**  
 Indica il nome del server di report. Nella maggior parte dei casi, si tratta del nome del computer in cui è installato il server di report.  
  
 **Istanza**  
 Indica il nome dell'istanza del server di report. Le istanze del server di report sono basate su istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Status**  
 Indica se il server di report è inizializzato o in attesa di essere unito a una distribuzione con scalabilità orizzontale:  
  
-   Per un server di report autonomo che non fa parte di una distribuzione con scalabilità orizzontale, questa pagina indica che l'istanza del server di report è inizializzata rispetto al relativo database del server di report dedicato. Lo stato è impostato su **Unione eseguita**.  
  
-   Per un server di report in attesa di essere unito a una distribuzione con scalabilità orizzontale, tale pagina contiene valori vuoti per Server, Istanza e Stato. Un server di report è in attesa di essere unito a distribuzione con scalabilità orizzontale se è stato selezionato un database del server di report esistente che è già utilizzato da un'altra istanza del server di report. Un messaggio in questa pagina indica di connettersi a un server di report già unito alla farm. Per completare questa richiesta, fare clic su **Connetti**, selezionare un server di report già inizializzato per l'utilizzo del database del server di report, fare clic su **Distribuzione con scalabilità orizzontale**, selezionare l'istanza del server di report impostata su **In attesa dell'unione**, quindi fare clic su **Inizializza**.  
  
-   Per un server di report che fa attualmente parte di una distribuzione con scalabilità orizzontale, in questa pagina viene visualizzato lo stato di inizializzazione di tutte le istanze del server di report che condividono lo stesso database del server di report. Le informazioni sullo stato visualizzate per una distribuzione con scalabilità orizzontale non dipendono dal server a cui si è connessi. Le informazioni sullo stato sono segnalate in modo identico per tutti i nodi nella distribuzione con scalabilità orizzontale.  
  
     Per un server di report che fa già parte di una distribuzione con scalabilità orizzontale, è possibile utilizzare questa pagina per aggiungere o rimuovere nodi.  
  
 **Inizializzare**  
 Fare clic su **Inizializza** per aggiungere un server di report alla distribuzione con scalabilità orizzontale. Questo passaggio consente di configurare un server di report per l'utilizzo di una chiave simmetrica in un database del server di report condiviso. È possibile utilizzare **Inizializza** per aggiungere un'istanza del server di report a una distribuzione con scalabilità orizzontale o per la risoluzione dei problemi di migrazione o installazione.  
  
 Un'istanza del server di report è disponibile solo se in precedenza è stata configurata una connessione al database condiviso del server di report. È necessario inoltre eseguire l'inizializzazione da un server di report già inizializzato per l'utilizzo del database del server di report.  
  
 **Rimuovi**  
 Fare clic su **Rimuovi** per rimuovere le chiavi di crittografia dell'istanza del server di report selezionata dal database del server di report. È possibile rimuovere le chiavi per rimuovere un server di report da una distribuzione con scalabilità orizzontale o per la risoluzione dei problemi di migrazione o installazione. Questa opzione fa sì che vengano rimosse solo le chiavi di crittografia relative all'istanza del server di report specificata. I dati crittografati nel database del server di report non vengono modificati.  
  
 A scopo cautelativo, accertarsi di creare una copia di backup della chiave simmetrica prima di rimuoverla. Dopo aver rimosso le chiavi di crittografia dell'ultimo server di report dell'elenco, specificare i nuovi requisiti per tutte le successive inizializzazioni del server di report per il database. In base al nuovo requisito, al termine dell'inizializzazione di un server di report è necessario ripristinare una copia di backup della chiave simmetrica. Il ripristino della chiave simmetrica è necessario per accedere ai dati crittografati attualmente archiviati nel database del server di report.  
  
 Se i dati crittografati non sono più necessari o se non si dispone di una copia di backup della chiave, sarà necessario eliminare i dati crittografati. Per ulteriori informazioni, vedere [chiavi di crittografia &#40;&#41;modalità nativa SSRS ](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzare un server di report &#40;Configuration Manager SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
  
  
