---
title: Stored procedure di gestione temporanea
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 103c43f012f6cf7025139fd29656a42d00fc233f
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727889"
---
# <a name="staging-stored-procedure-master-data-services"></a>Stored procedure di gestione temporanea (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Quando si inizia il processo di gestione temporanea da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], viene usata una delle tre stored procedure seguenti.  
  
-   stg.udp_\<name>_Leaf  
  
-   stg.udp_\<name>_Consolidated  
  
-   stg.udp_\<name>_Relationship  
  
 Dove name è il nome della tabella di staging specificata alla creazione dell'entità.  
  
## <a name="staging-process-stored-procedure-parameters"></a>Parametri delle stored procedure del processo di gestione temporanea  
 Nella tabella seguente vengono elencati i parametri di queste stored procedure.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|**VersionName**<br /><br /> Obbligatorio|Il nome della versione. Può supportare o non supportare la distinzione tra maiuscole e minuscole, a seconda dell'impostazione delle regole di confronto di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**LogFlag**<br /><br /> Obbligatorio|Determina se le transazioni sono registrate durante il processo di gestione temporanea. I valori possibili sono:<br /><br /> **0**: le transazioni non vengono registrate.<br /><br /> **1**: le transazioni vengono registrate.<br /><br /> <br /><br /> Per altre informazioni sulle transazioni, vedere [Transazioni &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md).|  
|**BatchTag**<br /><br /> Richiesto, salvo che dal servizio Web|Il valore **BatchTag** come specificato nella tabella di staging.|  
|**Batch_ID**<br /><br /> Richiesto solo dal servizio Web|Il valore **Batch_ID** come specificato nella tabella di staging.|  
|**Nome utente**|Parametro facoltativo|  
|**ID utente**|Parametro facoltativo|  
  
### <a name="staging-process-stored-procedure-example"></a>Esempio di stored procedure del processo di gestione temporanea  
 Nell'esempio seguente viene illustrata la modalità di inizio del processo di gestione temporanea mediante una stored procedure di gestione temporanea.  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
      @UserName=N'domain\user'  
  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di convalida &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [Visualizzare gli errori che si verificano durante il processo di gestione temporanea &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)  
  
  
