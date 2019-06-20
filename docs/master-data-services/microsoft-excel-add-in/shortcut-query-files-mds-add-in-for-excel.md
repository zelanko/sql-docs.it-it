---
title: File di query collegamento (componente aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 1ba0219a-6c40-41fa-aff9-8c8f41ef3220
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c02c20f55e6d814d2b1a95087f94da3824de57b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65486070"
---
# <a name="shortcut-query-files-mds-add-in-for-excel"></a>File di query collegamento (componente aggiuntivo MDS per Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Nel [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]usare i file di query collegamento per connettersi rapidamente e caricare i dati usati di frequente. È possibile utilizzarli anche quando si desidera condividere dati MDS con gli altri utenti. Anziché salvare il foglio di lavoro e inviarlo tramite posta elettronica, è necessario salvare un file di query collegamento e inviarlo tramite posta elettronica. In tal modo si assicura la connessione al repository MDS per il mittente e il destinatario in modo da ottenere gli ultimi dati.  
  
 I file di query collegamento sono file XML che contengono informazioni su:  
  
-   La connessione al repository MDS.  
  
-   Il modello, la versione e l'entità.  
  
-   Qualsiasi filtro applicato quando è stato creato il collegamento.  
  
-   L'ordine da sinistra a destra delle colonne quando è stato creato il collegamento.  
  
 È possibile salvare questi file in un elenco e scegliere quello desiderato quando si apre il componente aggiuntivo. È possibile esportarli nel proprio computer o in un percorso condiviso o è possibile inviarli ad altri utenti.  
  
 Per aprire i file di query collegamento è possibile procedere in due modi: importarli o fare doppio clic per aprirli automaticamente con l'applicazione QueryOpener.  
  
## <a name="queryopener-application"></a>Applicazione QueryOpener  
 Tutti gli utenti che installano [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] dispongono di un'applicazione, chiamata QueryOpener, installata. Questa applicazione è utilizzata per aprire i file di query collegamento in [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]. Se si fa doppio clic su un file di query collegamento, questa applicazione viene utilizzata automaticamente per aprire il file nel componente aggiuntivo.  
  
 Quando si apre un file di query collegamento con questa applicazione, viene richiesto di rendere la connessione "sicura", cioè si è sicuri del contenuto di questo percorso. Per impostare una connessione sicura, selezionare **Consenti sempre la connessione a questo indirizzo** nella finestra di richiesta. Ogni volta che si contrassegna una connessione come sicura, viene aggiunta a un elenco. Se si desidera deselezionare questo elenco, aprire la finestra di dialogo **Impostazioni** e nella sezione **Server aggiunti a elenco attendibili** , fare clic su **Deseleziona tutto**.  
  
 Il percorso predefinito per l'applicazione è *unità*:\Programmi\Microsoft SQL Server\130\Master Data Services\Excel Add-In\Microsoft.MasterDataServices.QueryOpener.exe.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Salvare il contenuto del foglio di lavoro attivo come file di query collegamento.|[Salvare un file di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Inviare tramite posta elettronica un file di query collegamento che rappresenta il contenuto del foglio di lavoro attivo.|[Inviare tramite posta elettronica un file di query collegamento &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Connessioni &#40;componente aggiuntivo MDS per Excel&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [Componente aggiuntivo Master Data Services per Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
-   [Sicurezza &#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
  
