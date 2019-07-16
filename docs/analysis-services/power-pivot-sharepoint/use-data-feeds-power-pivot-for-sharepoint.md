---
title: Usare feed di dati (Power Pivot per SharePoint) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 509d4a5293aef836f8ae9439ad7c8d315bbc790d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207977"
---
# <a name="use-data-feeds-power-pivot-for-sharepoint"></a>Usare feed di dati (PowerPivot per SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  I feed di dati rappresentano uno o più flussi di dati generati da un'origine dati online e trasmessi a un documento o a un'applicazione di destinazione. Se si usa [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel, i feed di dati consentono di trasferire dati di business o aziendali esistenti da origini dati arbitrarie alla finestra di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nella cartella di lavoro di Excel 2010. Dopo aver importato un feed di dati in una cartella di lavoro, è possibile farvi riferimento successivamente in qualsiasi operazione pianificata di aggiornamento dati in un server SharePoint.  
  
 La modalità di utilizzo di un feed di dati varia a seconda che si utilizzino funzionalità di esportazione predefinite in applicazioni che supportano feed di dati Atom oppure si creino e si utilizzino servizi di dati personalizzati. Le applicazioni che sono in grado di pubblicare e leggere i dati XML Atom offrono un trasferimento di dati continuo che nasconde agli utenti il metodo dei feed di dati e dei servizi dati. Per gli utenti si verifica un semplice spostamento di dati da un'applicazione a un'altra.  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e Microsoft SharePoint 2010 vengono forniti feed di dati da usare nelle cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . È possibile utilizzare le informazioni contenute in questo argomento per apprendere le modalità di accesso ai feed di dati da report ed elenchi già disponibili.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
 [Prerequisiti](#prereq)  
  
 [Creare un feed di dati da un elenco SharePoint](#sharepointlist)  
  
 [Creare un feed di dati da un report di Reporting Services](#rsreport)  
  
 [Creare un feed di dati da un documento di servizio dati](#dsdoc)  
  
##  <a name="prereq"></a> Prerequisiti  
 Per importare un feed di dati in Excel 2010 è necessario avere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel.  
  
 È necessario disporre di un servizio Web o di un servizio dati che consenta di fornire dati tabulari XML in formato Atom 1.0. I dati in questo formato possono essere forniti sia da [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sia da SharePoint 2010.  
  
 Prima di poter esportare un elenco SharePoint come un feed di dati, è necessario installare ADO.NET Data Services nel server SharePoint. Per altre informazioni, vedere [Installare ADO.NET Data Services per supportare esportazioni di feed di dati di elenchi SharePoint](http://msdn.microsoft.com/f32527ae-f623-4e08-adfb-6d3262f5c2ac).  
  
##  <a name="sharepointlist"></a> Creare un feed di dati da un elenco SharePoint  
 In una farm di SharePoint 2010 un elenco SharePoint dispone di un pulsante Esporta come feed di dati nella barra multifunzione dell'elenco. È possibile fare clic su questo pulsante per esportare l'elenco come feed. Per risultati ottimali, è necessario che nella workstation sia disponibile Excel 2010 con [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . L'applicazione client [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] verrà avviata in risposta all'esportazione dei feed di dati, creando una nuova tabella di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] contenente l'elenco.  
  
1.  Aprire l'elenco nel sito di SharePoint.  
  
2.  In Strumenti elenco fare clic su **Elenco**.  
  
3.  In Connetti ed esporta fare clic su **Esporta come feed di dati**.  
  
    > [!NOTE]  
    >  Il pulsante **Esporta come feed di dati** viene aggiunto a SharePoint con [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Se [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint non è installato o non è stata attivata la funzionalità [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , questo pulsante non sarà disponibile.  
  
4.  Fare clic su **Apri** se [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel è installato localmente o su **Salva** per salvare il documento con estensione atomsvc nell'unità disco rigido per operazioni di importazione successive.  
  
5.  Se si sceglie **Apri**, utilizzare l'Importazione guidata tabella per importare il feed di dati in un foglio di lavoro. Il feed di dati verrà aggiunto come nuova tabella nella finestra di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Si verificherà un errore se ADO.NET Data Services 3.5.1 non è installato nel server SharePoint. Per altre informazioni sull'errore e su come risolverlo, vedere [Installare ADO.NET Data Services per supportare esportazioni di feed di dati di elenchi SharePoint](http://msdn.microsoft.com/f32527ae-f623-4e08-adfb-6d3262f5c2ac).  
  
##  <a name="rsreport"></a> Creare un feed di dati da un report di Reporting Services  
 Se si dispone di una distribuzione di SQL Server 2008 R2 Reporting Services, è possibile utilizzare la nuova estensione per il rendering Atom per generare un feed di dati da un report esistente. Per risultati ottimali, è necessario che nella workstation sia disponibile Excel 2010 con [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel. L'applicazione client [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] verrà avviata in risposta all'esportazione dei feed di dati, aggiungendo e facendo riferimento automaticamente alle tabelle e alle colonne come sono state trasmesse.  
  
 Per istruzioni su come esportare un feed di dati da un report, vedere [Generare i feed di dati da un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md) nel [file della Guida di Generatore report](http://go.microsoft.com/fwlink/?LinkId=154494).  
  
> [!NOTE]  
>  Per impostare una pianificazione di aggiornamento dati ricorrente che consenta di importare nuovamente i dati del report in una cartella di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pubblicata in una raccolta di SharePoint, è necessario configurare il server di report per l'integrazione con SharePoint. Per altre informazioni sull'uso integrato di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint e Reporting Services, vedere [Configurazione e amministrazione di un server di report &#40;modalità SharePoint di Reporting Services&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md).  
  
##  <a name="dsdoc"></a> Creare un feed di dati da un documento di servizio dati  
 Se si dispone di un servizio dati personalizzato che consente di generare feed Atom, è possibile configurare un documento di servizio dati come metodo per rendere i dati disponibili a utenti e applicazioni. Un file *documento di servizio dati* (con estensione atomsvc) consente di specificare una o più connessioni a origini online tramite cui vengono pubblicati dati nel formato wire Atom. È possibile creare documenti di servizio dati in una *libreria feed di dati*, che rappresenta una libreria per scopi specifici che fornisce un punto di accesso comune per esplorare documenti di servizio dati pubblicati in un server di SharePoint. Gli information Worker che dispongono dell'autorizzazione per accedere ai documenti di servizio dati nella libreria feed di dati possono fare riferimento all'URL di SharePoint del documento per importare i feed di dati nelle cartelle di lavoro e nelle applicazioni in uso.  
  
1.  Aprire una libreria di feed di dati creata dall'amministratore del sito. Per altre informazioni, vedere [Creare o personalizzare una libreria di feed di dati &#40;PowerPivot per SharePoint&#41;;](../../analysis-services/power-pivot-sharepoint/create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md).  
  
2.  In Strumenti raccolta fare clic su **Documenti**.  
  
3.  Fare clic su **Nuovo documento**.  
  
4.  Fornire un nome di file e una descrizione.  
  
5.  Specificare uno o più URL che forniscono il feed:  
  
    1.  **URL di base** è facoltativo. È necessario specificare questo valore se un documento di servizio dati fornisce più feed. L'URL di base specifica la parte di URL comune a tutti i feed, ad esempio il nome del server e il sito. Se si crea un documento di servizio dati in un report di Reporting Services, l'URL di base sarà costituito dall'URL e dal report del server di report.  
  
    2.  **URL servizio Web** è obbligatorio. Senza l'URL di Base, questo valore deve includere `http://` o `https://` nell'indirizzo. Se è stato specificato un URL di base, l'URL servizio Web è costituito dalla parte che segue l'URL di base. Ad esempio, se l'URL completo è `http://adventure-works/inventory/today.aspx`, l'URL di Base sarà `http://adventure-works/inventory`, e l'URL del servizio Web sarà /today.aspx.  
  
         L'URL servizio Web può includere parametri che filtrano o selezionano un subset di dati. L'applicazione o il servizio che fornisce il feed deve supportare i parametri specificati nell'URL.  
  
6.  Immettere un valore in **Nome tabella**, una tabella per ogni feed. Questo valore è obbligatorio. Il nome della tabella viene utilizzato da un'applicazione client che utilizza il feed di dati. In [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel, il nome della tabella viene usato per denominare le tabelle nella finestra di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] che conterrà i dati importati.  
  
## <a name="see-also"></a>Vedere anche  
 [Attivare l'integrazione delle funzionalità di Power Pivot per le raccolte siti in Amministrazione centrale](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)   
 [Condividere feed di dati usando una libreria di feed di dati &#40;Power Pivot per SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint.md)  
  
  
