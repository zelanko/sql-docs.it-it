---
title: Usare feed di dati (PowerPivot per SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 50140fdf-6fd1-41a1-9c14-8ecfb97ba2e1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6efccad47f0d6670c87aeb1e9cc9ef9ec654a138
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070913"
---
# <a name="use-data-feeds-powerpivot-for-sharepoint"></a>Utilizzare feed di dati (PowerPivot per SharePoint)
  I feed di dati rappresentano uno o più flussi di dati generati da un'origine dati online e trasmessi a un documento o a un'applicazione di destinazione. Se si utilizza PowerPivot per Excel, i feed di dati consentono di trasferire i dati aziendali esistenti da origini dati arbitrarie in nella finestra di PowerPivot nella cartella di lavoro di Excel 2010. Dopo aver importato un feed di dati in una cartella di lavoro, è possibile farvi riferimento successivamente in qualsiasi operazione pianificata di aggiornamento dati in un server SharePoint.  
  
 La modalità di utilizzo di un feed di dati varia a seconda che si utilizzino funzionalità di esportazione predefinite in applicazioni che supportano feed di dati Atom oppure si creino e si utilizzino servizi di dati personalizzati. Le applicazioni che sono in grado di pubblicare e leggere i dati XML Atom offrono un trasferimento di dati continuo che nasconde agli utenti il metodo dei feed di dati e dei servizi dati. Per gli utenti si verifica un semplice spostamento di dati da un'applicazione a un'altra.  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e Microsoft SharePoint 2010 forniscono feed utilizzabili nelle cartelle di lavoro di PowerPivot di dati. È possibile utilizzare le informazioni contenute in questo argomento per apprendere le modalità di accesso ai feed di dati da report ed elenchi già disponibili.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Prerequisiti](#prereq)  
  
 [Creare un feed di dati da un elenco SharePoint](#sharepointlist)  
  
 [Creare un feed di dati da un report di Reporting Services](#rsreport)  
  
 [Creare un feed di dati da un documento di servizio dati](#dsdoc)  
  
##  <a name="prereq"></a> Prerequisiti  
 È necessario disporre di PowerPivot per Excel per importare un feed di dati in Excel 2010.  
  
 È necessario disporre di un servizio Web o di un servizio dati che consenta di fornire dati tabulari XML in formato Atom 1.0. I dati in questo formato possono essere forniti sia da [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sia da SharePoint 2010.  
  
 Prima di poter esportare un elenco SharePoint come un feed di dati, è necessario installare ADO.NET Data Services nel server SharePoint. Per altre informazioni, vedere [Installare ADO.NET Data Services per supportare esportazioni di feed di dati di elenchi SharePoint](../../sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).  
  
##  <a name="sharepointlist"></a> Creare un feed di dati da un elenco SharePoint  
 In una farm di SharePoint 2010 un elenco SharePoint dispone di un pulsante Esporta come feed di dati nella barra multifunzione dell'elenco. È possibile fare clic su questo pulsante per esportare l'elenco come feed. Per migliori risultati, è necessario che nella workstation sia disponibile Excel 2010 con l'applicazione client PowerPivot. L'applicazione client PowerPivot verrà avviata in risposta all'esportazione dei feed di dati, creando una nuova tabella di PowerPivot contenente l'elenco.  
  
1.  Aprire l'elenco nel sito di SharePoint.  
  
2.  In Strumenti elenco fare clic su **Elenco**.  
  
3.  In Connetti ed esporta fare clic su **Esporta come feed di dati**.  
  
    > [!NOTE]  
    >  Il **Esporta come Feed di dati** pulsante viene aggiunto a SharePoint tramite PowerPivot. Se PowerPivot per SharePoint non è installato o non è stata attivata la funzionalità di PowerPivot, questo pulsante non sarà disponibile.  
  
4.  Fare clic su **aperto** se PowerPivot per Excel è installato in locale o fare clic su **salvare** per salvare il documento con estensione atomsvc nell'unità disco rigido per operazioni di importazione in un secondo momento.  
  
5.  Se si sceglie **Apri**, utilizzare l'Importazione guidata tabella per importare il feed di dati in un foglio di lavoro. Il feed di dati verrà aggiunto come nuova tabella nella finestra di PowerPivot.  
  
 Si verificherà un errore se ADO.NET Data Services 3.5.1 non è installato nel server SharePoint. Per altre informazioni sull'errore e su come risolverlo, vedere [Installare ADO.NET Data Services per supportare esportazioni di feed di dati di elenchi SharePoint](../../sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).  
  
##  <a name="rsreport"></a> Creare un feed di dati da un report di Reporting Services  
 Se si dispone di una distribuzione di SQL Server 2008 R2 Reporting Services, è possibile utilizzare la nuova estensione per il rendering Atom per generare un feed di dati da un report esistente. Per risultati ottimali, è necessario che nella workstation sia disponibile Excel 2010 con PowerPivot per Excel. L'applicazione client PowerPivot verrà avviata in risposta all'esportazione dei feed di dati, aggiungendo e facendo riferimento automaticamente alle tabelle e alle colonne come sono state trasmesse.  
  
 Per istruzioni su come esportare un feed di dati da un report, vedere [Generare i feed di dati da un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md) nel [file della Guida di Generatore report](https://go.microsoft.com/fwlink/?LinkId=154494).  
  
> [!NOTE]  
>  Per impostare una pianificazione di aggiornamento dati ricorrente che consenta di importare nuovamente i dati del report in una cartella di lavoro di PowerPivot pubblicata in una raccolta di SharePoint, è necessario configurare il server di report per l'integrazione con SharePoint. Per altre informazioni sull'uso congiunto di PowerPivot per SharePoint e Reporting Services, vedere [configurazione e amministrazione di un Server di Report &#40;Reporting Services SharePoint Mode&#41;](../../reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md).  
  
##  <a name="dsdoc"></a> Creare un feed di dati da un documento di servizio dati  
 Se si dispone di un servizio dati personalizzato che consente di generare feed Atom, è possibile configurare un documento di servizio dati come metodo per rendere i dati disponibili a utenti e applicazioni. Un file *documento di servizio dati* (con estensione atomsvc) consente di specificare una o più connessioni a origini online tramite cui vengono pubblicati dati nel formato wire Atom. È possibile creare documenti di servizio dati in una *libreria feed di dati*, che rappresenta una libreria per scopi specifici che fornisce un punto di accesso comune per esplorare documenti di servizio dati pubblicati in un server di SharePoint. Gli information Worker che dispongono dell'autorizzazione per accedere ai documenti di servizio dati nella libreria feed di dati possono fare riferimento all'URL di SharePoint del documento per importare i feed di dati nelle cartelle di lavoro e nelle applicazioni in uso.  
  
1.  Aprire una libreria di feed di dati creata dall'amministratore del sito. Per altre informazioni, vedere [creare o personalizzare una libreria di Feed di dati &#40;PowerPivot per SharePoint&#41;](create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md).  
  
2.  In Strumenti raccolta fare clic su **Documenti**.  
  
3.  Fare clic su **Nuovo documento**.  
  
4.  Fornire un nome di file e una descrizione.  
  
5.  Specificare uno o più URL che forniscono il feed:  
  
    1.  **URL di base** è facoltativo. È necessario specificare questo valore se un documento di servizio dati fornisce più feed. L'URL di base specifica la parte di URL comune a tutti i feed, ad esempio il nome del server e il sito. Se si crea un documento di servizio dati in un report di Reporting Services, l'URL di base sarà costituito dall'URL e dal report del server di report.  
  
    2.  **URL servizio Web** è obbligatorio. Se l'URL di base questo valore deve includere http:// o https:// nell'indirizzo. Se è stato specificato un URL di base, l'URL servizio Web è costituito dalla parte che segue l'URL di base. Ad esempio, se l'URL completo è http://adventure-works/inventory/today.aspx, l'URL di Base sarà http://adventure-works/inventory, e l'URL del servizio Web sarà /today.aspx.  
  
         L'URL servizio Web può includere parametri che filtrano o selezionano un subset di dati. L'applicazione o il servizio che fornisce il feed deve supportare i parametri specificati nell'URL.  
  
6.  Immettere un valore in **Nome tabella**, una tabella per ogni feed. Questo valore è obbligatorio. Il nome della tabella viene utilizzato da un'applicazione client che utilizza il feed di dati. In PowerPivot per Excel, il nome della tabella viene utilizzato per denominare le tabelle nella finestra di PowerPivot che conterrà i dati importati.  
  
## <a name="see-also"></a>Vedere anche  
 [Attivare integrazione delle funzionalità di PowerPivot per le raccolte siti in Amministrazione centrale](activate-power-pivot-integration-for-site-collections-in-ca.md)   
 [Condividere feed di dati usando una libreria di Feed di dati &#40;PowerPivot per SharePoint&#41;](share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint.md)  
  
  
