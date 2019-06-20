---
title: Componente aggiuntivo Master Data Services per Microsoft Excel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d8bac9ba8afafa6b5141d90c51f8029f596ba8f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482618"
---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>Componente aggiuntivo Master Data Services per Microsoft Excel
  Con il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], elenchi principali di dati di riferimento possono essere distribuiti a ogni persona dell'organizzazione che usa Excel. La sicurezza determina quali utenti dei dati possono eseguire operazioni di visualizzazione e aggiornamento.  
  
 È possibile caricare gli elenchi filtrati di dati da MDS in Excel, dove è possibile usarlo come qualsiasi altro tipo di dati. Una volta completata l'operazione, è possibile pubblicare di nuovo i dati in MDS, dove vengono archiviati centralmente.  
  
 Se si è un amministratore, è possibile usare [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] per creare entità e attributi e caricarli con i dati. In questo modo viene eliminata la necessità di usare altri strumenti per caricare i dati nei modelli.  
  
 In [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]è possibile utilizzare Data Quality Services (DQS) per la corrispondenza dei dati prima del caricamento in MDS. In tal modo si impedisce la duplicazione dei dati in MDS.  
  
> [!IMPORTANT]  
>  È possibile continuare a usare la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 del componente aggiuntivo Master Data Services per Excel dopo l'aggiornamento di Master Data Services e di Data Quality Services a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Tuttavia, una versione precedente del componente aggiuntivo Master Data Services per Excel non funzionerà dopo l'aggiornamento a SQL Server 2014 CTP2. È possibile scaricare la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 del componente aggiuntivo Master Data Services per Excel da [qui](https://go.microsoft.com/fwlink/?LinkId=328664).  
  
## <a name="terms"></a>Termini  
 Quando si utilizza il componente aggiuntivo, è possibile incontrare i termini seguenti.  
  
-   Il *MDS repository* in cui vengono memorizzati tutti i dati master. È un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurato per archiviare dati MDS. Per usare dati provenienti dal repository, caricarli in Excel. Dopo averli usati, pubblicare di nuovo le modifiche nel repository. Gli amministratori possono aggiungere nuove entità e attributi al repository.  
  
-   I*dati gestiti tramite MDS* sono dati archiviati nel repository MDS che vengono caricati in Excel, dove vengono visualizzati come righe evidenziate. È possibile aggiungere dati che non sono gestiti da MDS al foglio di lavoro, senza che quest'ultimo venga modificato quando si aggiornano i dati gestiti da MDS.  
  
-   Un *model* è un contenitore di dati. È possibile creare versioni di questi contenitori e generalmente l'ultima versione è la più recente. Per altre informazioni, vedere [Modelli &#40;Master Data Services&#41;](../models-master-data-services.md).  
  
-   Un oggetto *entity* è un elenco di dati. Un'entità può essere considerata come una tabella in un database. È possibile, ad esempio, che un'entità **Color** contenga un elenco di colori. Per altre informazioni, vedere [Entità &#40;Master Data Services&#41;](../entities-master-data-services.md).  
  
-   Un *member* è una riga di dati. Ogni entità contiene membri. Un esempio di un membro è **Blu**. Per altre informazioni, vedere [Membri &#40;Master Data Services&#41;](../members-master-data-services.md).  
  
-   Un *attribute* è una colonna di dati. Ogni membro dispone di attributi. Ad esempio, l'attributo **Code** per il membro **Blue** è **B**. Per altre informazioni sugli attributi, vedere [Attributi &#40;Master Data Services&#41;](../attributes-master-data-services.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Creare una connessione a un repository [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Connettersi a un repository MDS &#40;componente aggiuntivo MDS per Excel&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|Caricare dati gestiti da MDS in Excel.|[Caricare i dati da MDS in Excel](export-data-to-excel-from-master-data-services.md)|  
|Salvare una query di collegamento che è possibile usare per aprire i dati gestiti da MDS attualmente visualizzati in seguito.|[Salvare un file di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Condividere collegamenti con gli altri.|[Inviare tramite posta elettronica un file di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Visualizzare tutte le modifiche apportate a un membro.|[Visualizzare tutte le annotazioni o transazioni per un membro &#40;componente aggiuntivo MDS per Excel&#41;](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|Prima di pubblicare nuovi dati, verificare se esistono duplicati.|[Cercare la corrispondenza tra dati simili &#40;componente aggiuntivo MDS per Excel&#41;](match-similar-data-mds-add-in-for-excel.md)|  
|Pubblicare dati da un foglio di lavoro nel repository MDS.|[Pubblicare dati da Excel a MDS &#40;componente aggiuntivo MDS per Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Creare una nuova entità con i dati nel foglio di lavoro. (Solo amministratori).|[Creare un'entità &#40;componente aggiuntivo MDS per Excel&#41;](create-an-entity-mds-add-in-for-excel.md)|  
|Creare un attributo basato sul dominio, anche noto come un elenco vincolato. (Solo amministratori).|[Creare un attributo basato su dominio &#40;componente aggiuntivo MDS per Excel&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Impostare le proprietà per il caricamento e la pubblicazione di dati nel componente aggiuntivo Master Data Services per Excel. (Solo amministratori).|[Impostazione delle proprietà per il componente aggiuntivo Master Data Services per Excel](setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Connessioni &#40;componente aggiuntivo MDS per Excel&#41;](connections-mds-add-in-for-excel.md)  
  
-   [Il caricamento dei dati &#40;componente aggiuntivo MDS per Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [File di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Corrispondenza Data Quality nel componente aggiuntivo MDS per Excel](data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [Pubblicazione di dati &#40;componente aggiuntivo MDS per Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [Compilazione di un modello &#40;componente aggiuntivo MDS per Excel&#41;](building-a-model-mds-add-in-for-excel.md)  
  
-   [Sicurezza &#40;Master Data Services&#41;](../security-master-data-services.md)  
  
  
