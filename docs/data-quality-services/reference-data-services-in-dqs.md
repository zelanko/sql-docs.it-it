---
description: Servizi dati di riferimento in DQS
title: Servizi dati di riferimento in DQS
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ef217717-6d05-443e-af26-44dc745a349d
author: swinarko
ms.author: sawinark
ms.openlocfilehash: e382be5f109efff9a0a08eb434017334fe54d2c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466736"
---
# <a name="reference-data-services-in-dqs"></a>Servizi dati di riferimento in DQS

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  I dati di riferimento sono un set accurato e completo di dati globali correlati o categorizzati (oltre i limiti di un'impresa) disponibile presso domini pubblici attendibili o da provider premium di contenuti commerciali.  
  
 La funzionalità relativa ai servizi dati di riferimento in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) consente di sottoscrivere a provider di dati di riferimento di terze parti per pulire e arricchire con facilità i dati aziendali convalidandoli mediante confronto con dati di alta qualità. È possibile utilizzare i servizi offerti da provider leader nei servizi di qualità dei dati dall'interno di DQS, in modo da standardizzare, correggere o arricchire i dati durante il processo di pulizia. È ad esempio possibile confrontare un elenco di codici postali o CAP con i relativi dati di riferimento per convalidare gli indirizzi dei clienti.  
  
 La funzionalità per il servizio dati di riferimento presenta i vantaggi seguenti:  
  
-   I dati di riferimento consentono di garantire la qualità dei dati confrontandoli con dati garantiti da una società di terze parti.  
  
-   Il processo relativo ai dati di riferimento è incorporato nella compilazione della Knowledge Base di DQS e nei progetti di qualità dei dati, consentendo di istituire un processo della qualità dei dati completo.  
  
-   Supporta l'uso di dati di riferimento da Azure Marketplace e direttamente da provider di dati di riferimento di terze parti.  
  
##  <a name="using-reference-data-from-azure-marketplace"></a><a name="Marketplace"></a> Uso dei dati di riferimento da Azure Marketplace  
 DQS supporta l'utilizzo di dati di riferimento da Azure Marketplace per consentire ai provider di contenuti di fornire servizi dati di riferimento tramite il Marketplace. Marketplace è un servizio Microsoft che fornisce un singolo marketplace e canale di recapito per dati e applicazioni di alta qualità come servizi cloud. Per ulteriori informazioni su Marketplace, vedere informazioni [sulle Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/about) ( https://azuremarketplace.microsoft.com/about) .
  
 La perfetta integrazione tra Marketplace e DQS semplifica i passaggi associati all'individuazione, all'esplorazione e all'acquisizione di informazioni per i progetti Data Quality dall'interno di DQS. I dati vengono utilizzati in DQS e aiutano gli utenti di DQS a ottenere un'elevata qualità dei dati unendo in modo del tutto innovativo le funzionalità di DQS, Marketplace e dei provider di servizi dati di riferimento.  
  
 Per utilizzare dati di riferimento da Marketplace in DQS per l'attività di pulizia, è necessario avere una chiave account Marketplace. La creazione di una chiave account Marketplace è gratuita ed è richiesto un pagamento solo se si richiedono set di dati a pagamento. Non vi sono spese per la sottoscrizione né per l'utilizzo di set di dati gratuiti. Per informazioni dettagliate sulla creazione di una chiave account Marketplace, vedere [creare un account](https://go.microsoft.com/fwlink/?LinkId=212936) ( https://go.microsoft.com/fwlink/?LinkId=212936) .  
  
 È inoltre possibile eseguire le seguenti attività Marketplace dall'interno di DQS:  
  
-   Sfogliare set di dati in Marketplace.  
  
-   Creare una chiave account Marketplace.  
  
-   Gestire i dettagli dell'account Marketplace, ad esempio chiavi account e sottoscrizioni ai provider di dati.  
  
 È possibile eseguire tali attività nella scheda **Dati di riferimento** della schermata **Configurazione** in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
##  <a name="using-reference-data-directly-from-the-third-party-reference-data-providers"></a><a name="Direct"></a> Utilizzo dei dati di riferimento direttamente dai provider di dati di riferimento di terze parti  
 Se non si è connessi a Internet, e quindi non è possibile usare Marketplace, DQS supporta anche la connessione diretta a provider di dati disponibili all'interno della rete della propria organizzazione. Per utilizzare dati di riferimento da provider di dati di riferimento di terze parti online, è necessario creare un record per il provider di dati in DQS.  
  
##  <a name="how-to-cleanse-data-by-using-the-reference-data"></a><a name="HowToCleanse"></a> Come pulire i dati utilizzando i dati di riferimento  
 La pulizia dei dati in DQS utilizzando dati di riferimento prevede i tre passaggi seguenti:  
  
1.  **Configurazione dei dettagli del provider di dati di riferimento in DQS**: prima che sia possibile utilizzare dati di riferimento in DQS, è necessario configurare i dettagli del servizio dati di riferimento in DQS.  
  
    1.  Se si usa Marketplace, fornire una chiave account Marketplace valida, passare alla categoria di dati [Data Services](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=data-services) in Marketplace e sottoscrivere i provider richiesti.  
  
    2.  Se si utilizza un provider di dati di riferimento online diretto, è necessario aggiungere i dettagli diretti del provider di dati di riferimento in DQS prima che sia possibile utilizzarlo.  
  
     La configurazione dei dettagli del provider di dati di riferimento in DQS è un'attività che si esegue una sola volta per ogni provider di dati specifico. Solo gli amministratori DQS possono configurare le impostazioni relative ai dati di riferimento in DQS.  
  
2.  **Eseguire il mapping di un dominio/dominio composito in una Knowledge Base al servizio dati di riferimento**: eseguire il mapping di un dominio/dominio composito al servizio dati di riferimento appropriato sottoscritto/aggiunto nel passaggio 1.  
  
3.  **Utilizzare i domini con mapping per l'attività Pulizia in un progetto Data Quality**: durante la creazione di un progetto Data Quality per l'attività **Pulizia** , selezionare la Knowledge Base che contiene i domini/domini compositi di cui è stato eseguito il mapping ai servizi dati di riferimento nel passaggio 2 ed eseguire l'attività di pulizia.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritto come configurare DQS per utilizzare servizi dati di riferimento da Marketplace o da provider diretti di dati di terze parti online.|[Configurazione di DQS per l'utilizzo di dati di riferimento](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|Viene descritto come eseguire il mapping di un dominio/dominio composito in una Knowledge Base a un servizio dati di riferimento.|[Collegare un dominio o un dominio composito ai dati di riferimento](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|Viene descritto come pulire i dati utilizzando un servizio dati di riferimento.|[Pulire i dati mediante le informazioni dei dati di riferimento &#40;esterni&#41;](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
  
  
