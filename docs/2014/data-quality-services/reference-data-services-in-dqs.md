---
title: Servizi dati di riferimento in DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ef217717-6d05-443e-af26-44dc745a349d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4b1a5d1aa7c35455e83361e2c04a686a75713574
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56038352"
---
# <a name="reference-data-services-in-dqs"></a>Servizi dati di riferimento in DQS
  I dati di riferimento sono un set accurato e completo di dati globali correlati o categorizzati (oltre i limiti di un'impresa) disponibile presso domini pubblici attendibili o da provider premium di contenuti commerciali.  
  
 La funzionalità relativa ai servizi dati di riferimento in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) consente di sottoscrivere a provider di dati di riferimento di terze parti per pulire e arricchire con facilità i dati aziendali convalidandoli mediante confronto con dati di alta qualità. È possibile utilizzare i servizi offerti da provider leader nei servizi di qualità dei dati dall'interno di DQS, in modo da standardizzare, correggere o arricchire i dati durante il processo di pulizia. È ad esempio possibile confrontare un elenco di codici postali o CAP con i relativi dati di riferimento per convalidare gli indirizzi dei clienti.  
  
 La funzionalità per il servizio dati di riferimento presenta i vantaggi seguenti:  
  
-   I dati di riferimento consentono di garantire la qualità dei dati confrontandoli con dati garantiti da una società di terze parti.  
  
-   Il processo relativo ai dati di riferimento è incorporato nella compilazione della Knowledge Base di DQS e nei progetti di qualità dei dati, consentendo di istituire un processo della qualità dei dati completo.  
  
-   La funzionalità supporta l'utilizzo di dati di riferimento da Windows Azure Marketplace e direttamente dai provider di dati di riferimento di terze parti.  
  
##  <a name="Marketplace"></a> Utilizzo dei dati di riferimento da Windows Azure Marketplace  
 DQS supporta l'utilizzo di dati di riferimento da Windows Azure Marketplace per consentire ai provider di contenuti di fornire servizi dati di riferimento mediante il servizio Marketplace. Marketplace è un servizio Microsoft che fornisce un singolo marketplace e canale di recapito per dati e applicazioni di alta qualità come servizi cloud. Per altre informazioni su Marketplace, vedere [Learn About Windows Azure Marketplace](https://go.microsoft.com/fwlink/?LinkId=211291) (Informazioni su Windows Azure Marketplace) (https://go.microsoft.com/fwlink/?LinkId=211291).  
  
 La perfetta integrazione tra Marketplace e DQS semplifica i passaggi associati all'individuazione, all'esplorazione e all'acquisizione di informazioni per i progetti Data Quality dall'interno di DQS. I dati vengono utilizzati in DQS e aiutano gli utenti di DQS a ottenere un'elevata qualità dei dati unendo in modo del tutto innovativo le funzionalità di DQS, Marketplace e dei provider di servizi dati di riferimento.  
  
 Per utilizzare dati di riferimento da Marketplace in DQS per l'attività di pulizia, è necessario avere una chiave account Marketplace. La creazione di una chiave account Marketplace è gratuita ed è richiesto un pagamento solo se si richiedono set di dati a pagamento. Non vi sono spese per la sottoscrizione né per l'utilizzo di set di dati gratuiti. Per informazioni dettagliate sulla creazione di una chiave account Marketplace, vedere [Creazione di un account](https://go.microsoft.com/fwlink/?LinkId=212936) (https://go.microsoft.com/fwlink/?LinkId=212936).  
  
 È inoltre possibile eseguire le seguenti attività Marketplace dall'interno di DQS:  
  
-   Sfogliare set di dati in Marketplace.  
  
-   Creare una chiave account Marketplace.  
  
-   Gestire i dettagli dell'account Marketplace, ad esempio chiavi account e sottoscrizioni ai provider di dati.  
  
 È possibile eseguire tali attività nella scheda **Dati di riferimento** della schermata **Configurazione** in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
##  <a name="Direct"></a> Utilizzo dei dati di riferimento direttamente dai provider di dati di riferimento di terze parti  
 Se non si è connessi a Internet, e quindi non è possibile usare Marketplace, DQS supporta anche la connessione diretta a provider di dati disponibili all'interno della rete della propria organizzazione. Per utilizzare dati di riferimento da provider di dati di riferimento di terze parti online, è necessario creare un record per il provider di dati in DQS.  
  
##  <a name="HowToCleanse"></a> Come pulire i dati utilizzando i dati di riferimento  
 La pulizia dei dati in DQS utilizzando dati di riferimento prevede i tre passaggi seguenti:  
  
1.  **Configurare i dettagli del provider di dati di riferimento in DQS**: Prima che sia possibile utilizzare i dati di riferimento in DQS, è necessario configurare i dettagli del servizio dati di riferimento in DQS.  
  
    1.  Se si utilizza Marketplace, fornire una chiave account Marketplace valida, passare alla categoria dati [Data Quality Services](https://go.microsoft.com/fwlink/?LinkId=227587) in Marketplace, quindi effettuare la sottoscrizione ai provider desiderati.  
  
    2.  Se si utilizza un provider di dati di riferimento online diretto, è necessario aggiungere i dettagli diretti del provider di dati di riferimento in DQS prima che sia possibile utilizzarlo.  
  
     La configurazione dei dettagli del provider di dati di riferimento in DQS è un'attività che si esegue una sola volta per ogni provider di dati specifico. Solo gli amministratori DQS possono configurare le impostazioni relative ai dati di riferimento in DQS.  
  
2.  **Eseguire il mapping di un dominio/dominio composito in una knowledge base per il servizio dati di riferimento**: Eseguire il mapping di un dominio/dominio composito al servizio dati di riferimento appropriato sottoscritto/aggiunto nel passaggio 1.  
  
3.  **Usare i domini con mapping per l'attività di pulizia in un progetto data quality**: Durante la creazione di un progetto data quality per la **pulizia** attività, selezionare la knowledge base che contiene domini/domini compositi mappati ai servizi dati di riferimento nel passaggio 2 ed eseguire l'attività di pulizia.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritto come configurare DQS per utilizzare servizi dati di riferimento da Marketplace o da provider diretti di dati di terze parti online.|[Configurare DQS per l'uso di dati di riferimento](../../2014/data-quality-services/configure-dqs-to-use-reference-data.md)|  
|Viene descritto come eseguire il mapping di un dominio/dominio composito in una Knowledge Base a un servizio dati di riferimento.|[Collegare un dominio o un dominio composito ai dati di riferimento](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)|  
|Viene descritto come pulire i dati utilizzando un servizio dati di riferimento.|[Pulire i dati mediante le informazioni dei dati di riferimento &#40;esterni&#41;](../../2014/data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
  
  
