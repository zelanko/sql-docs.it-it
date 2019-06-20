---
title: Connessioni (componente aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 2f2b2f9d-7744-460e-83cd-56d34ea70ff0
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 534d636aeb7c6b974ab98b8f651b5c21761ba934
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488395"
---
# <a name="connections-mds-add-in-for-excel"></a>Connessioni (componente aggiuntivo MDS per Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Per scaricare dati nel [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]è necessario prima creare una connessione. Una connessione è la modalità con cui un servizio Web [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] individua il database MDS a cui connettersi.  
  
 La stringa di connessione è generalmente l'URL dell'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], ad esempio `https://contoso/mds`.  
  
 Ogni volta che si avvia Excel, è necessario connettersi a un repository MDS. L'unica eccezione è quando il foglio di calcolo attivo già contiene i dati gestiti da MDS. In questo caso, si stabilisce automaticamente una connessione ogni volta che si aggiornano o pubblicano dati nel foglio.  
  
 È possibile creare più connessioni. La connessione alla quale si è effettuato l'accesso più recentemente è considerata il valore predefinito.  
  
 È possibile connettere più utenti contemporaneamente. Tuttavia, si possono verificare conflitti quando più utenti tentano di pubblicare gli stessi dati. Per altre informazioni, vedere [Panoramica: Importazione di dati da Excel &#40;Componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md).  
  
## <a name="connect-automatically-and-load-frequently-used-data"></a>Connettersi automaticamente e caricare i dati utilizzati frequentemente  
 Se si desidera connettersi sempre allo stesso server e caricare lo stesso set di dati, è possibile creare file di query collegamento che contengano la connessione e filtrino le informazioni. Per altre informazioni sui file di query, vedere [File di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md).  
  
## <a name="data-quality-services"></a>Data Quality Services  
 Il [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] dispone della funzionalità Data Quality Services per consentire la corrispondenza dei dati prima di pubblicarli nel repository MDS. Quando si stabilisce una connessione, se un database DQS è installato sulla stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come database MDS, sarà possibile visualizzare i pulsanti DQS sulla barra multifunzione. Se il database DQS_Main non esiste nell'istanza, questi pulsanti non sono visualizzati e la funzionalità Data Quality non è disponibile.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Creare una connessione a un database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Connettersi a un repository MDS &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|Caricare dati MDS in Excel.|[Esportare dati in Excel da Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|Filtrare i dati MDS prima di caricarli in Excel.|[Filtrare i dati prima dell'esportazione &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Panoramica: Esportazione dei dati in Excel &#40;componente aggiuntivo Master Data Services per Microsoft Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [File di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Componente aggiuntivo Master Data Services per Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
  
