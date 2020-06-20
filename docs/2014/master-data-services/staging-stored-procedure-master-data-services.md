---
title: Stored procedure di gestione temporanea (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9259352350a099db5d9b18411ad4da06dfb19819
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971071"
---
# <a name="staging-stored-procedure-master-data-services"></a>Stored procedure di gestione temporanea (Master Data Services)
  Quando si inizia il processo di gestione temporanea da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], viene usata una delle tre stored procedure seguenti.  
  
-   stg.udp_name_Leaf  
  
-   stg.udp_name_Consolidated  
  
-   stg.udp_name_Relationship  
  
 Dove name è il nome della tabella di staging specificata alla creazione dell'entità.  
  
## <a name="staging-process-stored-procedure-parameters"></a>Parametri delle stored procedure del processo di gestione temporanea  
 Nella tabella seguente vengono elencati i parametri di queste stored procedure.  
  
|Parametro|Description|  
|---------------|-----------------|  
|**VersionName**<br /><br /> Obbligatoria|Il nome della versione. Può supportare o non supportare la distinzione tra maiuscole e minuscole, a seconda dell'impostazione delle regole di confronto di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**LogFlag**<br /><br /> Obbligatoria|Determina se le transazioni sono registrate durante il processo di gestione temporanea. I valori possibili sono:<br /><br /> **0**: le transazioni non vengono registrate.<br />**1**: le transazioni vengono registrate.<br /><br /> <br /><br /> Per altre informazioni sulle transazioni, vedere [Transazioni &#40;Master Data Services&#41;](transactions-master-data-services.md).|  
|**BatchTag**<br /><br /> Richiesto, salvo che dal servizio Web|Il valore **BatchTag** come specificato nella tabella di staging.|  
|**Batch_ID**<br /><br /> Richiesto solo dal servizio Web|Il valore **Batch_ID** come specificato nella tabella di staging.|  
  
### <a name="staging-process-stored-procedure-example"></a>Esempio di stored procedure del processo di gestione temporanea  
 Nell'esempio seguente viene illustrata la modalità di inizio del processo di gestione temporanea mediante una stored procedure di gestione temporanea.  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [&#40;della stored procedure di convalida Master Data Services&#41;](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)   
 [Caricare o aggiornare membri in Master Data Services tramite il processo di gestione temporanea](add-update-and-delete-data-master-data-services.md)   
 [Visualizzare gli errori che si verificano durante il processo di gestione temporanea &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)  
  
  
