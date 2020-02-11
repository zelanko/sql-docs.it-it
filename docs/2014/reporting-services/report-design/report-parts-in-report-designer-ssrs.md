---
title: Parti del report in Progettazione report (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.components.f1
ms.assetid: 0c34311d-05d6-4bd2-b452-545fa95f8e7f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c696b87a8c8cf4688e24a0e3177948d339d7443
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105056"
---
# <a name="report-parts-in-report-designer-ssrs"></a>Parti del report in Progettazione report (SSRS)
  In Progettazione report, dopo aver creato tabelle, grafici e altri elementi del report in un progetto, è possibile pubblicarli come *parti di report* in un server di report o in un sito di SharePoint integrato con un server di report in modo da permetterne il riutilizzo in altri report.  
  
 In termini generali il funzionamento delle parti di report in Progettazione report e in Generatore report è identico. Per informazioni sulle funzionalità di base, vedere [parti del Report &#40;Generatore report e SSRS&#41;](../report-parts-report-builder-and-ssrs.md) nella [documentazione di Generatore report](https://go.microsoft.com/fwlink/?LinkId=154494) in MSDN.Microsoft.com.  
  
 Esistono differenze fondamentali nel modo in cui le parti di report funzionano in Progettazione report, quale ad esempio il flusso di lavoro. Generatore report consente di eseguire la creazione in collaborazione, vale a dire la creazione e la pubblicazione da parte di un utente di una parte di report che potrà essere riutilizzata, modificata e ripubblicata da un altro utente. In Progettazione report la pubblicazione è unidirezionale, cioè un utente può pubblicare una parte di report da Progettazione report e un altro può riutilizzarla. Tuttavia, il primo utente non può riutilizzare una parte di report esistente in un report disponibile in Progettazione report. In questo argomento, dopo una veloce panoramica delle parti di report, vengono illustrate queste differenze.  
  
##  <a name="ComponentWorkflow"></a>Ciclo di vita della pubblicazione di una parte di report  
 ![rs_ComponentCreation](../media/rs-componentcreation.gif "rs_ComponentCreation")  
  
1.  In Progettazione report un utente A crea un progetto contenente un report con un grafico che dipende da un set di dati incorporato.  
  
2.  L'utente A contrassegna il grafico con il set di dati incorporato per la pubblicazione. Al grafico viene automaticamente assegnato un ID univoco. L'utente A distribuisce quindi il report al server di report. Il grafico viene pubblicato in Progettazione report.  
  
3.  Un utente B crea un report vuoto in Generatore report e vi aggiunge il grafico. A questo punto il grafico è parte del report dell'utente B, insieme al set di dati incorporato. L'utente B può modificare le istanze del grafico e del set di dati contenuti nel report. Questa operazione non avrà effetto sulle istanze del grafico e del set di dati sul server di report, né interromperà la relazione tra le istanze nel report e sul server di report.  
  
     ![rs_BIDScomponentupdate](../media/rs-bidscomponentupdate.gif "rs_BIDScomponentupdate")  
  
4.  In Progettazione report l'utente A modifica il grafico nel report originale.  
  
5.  L'utente A ridistribuisce il report determinando in tal modo la ripubblicazione e il conseguente aggiornamento del grafico nel server.  
  
6.  In Generatore report l'utente B accetta il grafico aggiornato dal server. sovrascrivendo così le modifiche che l'utente B ha apportato al grafico nel report dell'utente B.  
  
##  <a name="PublishingComponents"></a>Pubblicazione di parti di report  
 Quando si pubblica una parte di report, in Progettazione report viene assegnato un ID univoco alla parte. Questo ID non subisce modifiche anche nel caso in cui si apportino modifiche successive alla parte. L'ID consente di collegare l'elemento del report originale nel report alla parte di report. Quando altri autori del report riutilizzano la parte di report in Generatore report, tramite l'ID è anche possibile collegare la parte di report nel report in uso al server di report.  
  
 È possibile pubblicare come parti di report gli elementi di report riportati di seguito.  
  
-   Grafici  
  
-   Misuratori  
  
-   Immagini e immagini incorporate  
  
-   Mappe  
  
-   Parametri  
  
-   Rettangoli  
  
-   Tabelle  
  
-   Matrici  
  
-   Elenchi  
  
 Se si pubblica una parte di report in cui vengono visualizzati dati, quali una tabella, una matrice o un grafico, è possibile basarla su un set di dati condiviso; in caso contrario, quando si pubblica la parte di report, il set di dati dal quale dipende viene salvato come set di dati incorporato. I set di dati incorporati possono essere basati su origini dati incorporate, ma le credenziali non vengono archiviate nelle origini dati incorporate. Pertanto, se la parte di report dipende da un set di dati incorporato che utilizza un'origine dati incorporata, chiunque la riutilizzi dovrà fornire le credenziali per l'origine dati incorporata. Per evitare questo problema, basare i set di dati incorporati e condivisi su origini dati condivise con credenziali archiviate. Per ulteriori informazioni, vedere [parti del report e set di dati in Generatore report](../report-data/report-parts-and-datasets-in-report-builder.md) nella [documentazione di Generatore report](https://go.microsoft.com/fwlink/?LinkId=154494) in MSDN.Microsoft.com.  
  
 La pubblicazione di una parte di report in Progettazione report viene eseguita in due passaggi:  
  
1.  Contrassegnare gli elementi di report che si desidera pubblicare nella finestra di dialogo **Pubblica parti di report** .  
  
2.  Distribuire il report.  
  
 Quando si distribuisce il report, la parte di report viene pubblicata in un sito di SharePoint o in un server di report e altri utenti possono riutilizzarla. Per pubblicare una parte di report, è necessario avere effettuato la connessione a un server di report di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e disporre di autorizzazioni sufficienti per la distribuzione del report.  
  
  
##  <a name="SearchReuseComponents"></a>Riutilizzo di parti di report  
 Diversamente da Generatore report, non è possibile cercare e riutilizzare una parte di report in un progetto diverso da quello in cui è stato creato.  
  
 Gli autori di report che utilizzano Generatore report possono cercare e riutilizzare le parti di report pubblicate nei report che creano.  
  
##  <a name="RepublishingComponents"></a>Ripubblicazione di parti di report  
 In Progettazione report è necessario aggiornare una parte di report esistente dall'interno del report nel quale è stata creata. In Generatore report gli autori del report possono riutilizzare la parte di report e pubblicarla coma una nuova parte senza sostituire la parte di report pubblicata. Se dispongono di autorizzazioni sufficienti possono anche aggiornare la parte di report pubblicata. Le parti di report archiviate in una cartella su un sito o sul server possono essere aggiornate da qualsiasi utente dotato di autorizzazioni sufficienti. L'ultimo aggiornamento sovrascrive gli aggiornamenti precedenti.  
  
 È possibile modificare e poi ripubblicare la parte di report nel sito o nel server. In Generatore report gli autori del report che hanno aggiunto la parte a un report vengono informati della modifica alla successiva apertura del report e possono accettare o meno le modifiche.  
  
 È inoltre possibile scegliere di pubblicare come nuovo un report già pubblicato. Nella finestra di dialogo Pubblica parti del report, fare clic su Pubblica come nuova parte del report. In questa nuova parte del report è disponibile un nuovo ID univoco e non presenta alcuna relazione con la parte vecchia del report.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di parti di report](managing-report-parts.md)  
  
  
