---
title: Tipi di dati di SQL Server e SSIS supportati per i domini DQS | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: fb1229b0eced2e48279bca5491b0ad9e46cc04aa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469200"
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>Tipi di dati di SQL Server e SSIS supportati per i domini DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Esistono molti tipi di dati in SQL Server e SQL Server Integration Services (SSIS), ma solo quattro tipi di dati per i domini DQS: Date, Decimal, Integer e String. No tutti i tipi di dati di SQL Server e SSIS sono supportati in DQS. È possibile eseguire il mapping dei dati di origine a un dominio DQS per eseguire le attività per la qualità dei dati solo se il tipo di dati di origine è supportato in DQS e corrisponde al tipo di dati del dominio DQS. In questo argomento vengono fornite informazioni sui tipi di dati supportati in SQL Server e SSIS e disponibili per l'esecuzione del mapping a ognuno dei quattro tipi di dati del dominio in DQS.  
  
> [!NOTE]  
>  Nei file XLSX e XLS il tipo di dati della colonna di origine viene determinato dal tipo di dati più prevalente nelle prime otto righe. Se una cella non è conforme a tale tipo di dati, verrà fornito un valore Null. In modo simile, nei file CSV, il tipo di dati della colonna di origine viene determinato dal tipo di dati più prevalente nelle prime otto righe.  
  
##  <a name="SQLServer"></a> Tipi di dati di SQL Server supportati  
 Nella seguente tabella vengono fornite informazioni sui tipi di dati supportati in SQL Server per ogni tipo di dati del dominio DQS:  
  
|Tipo di dati del dominio DQS.|Tipo di dati di SQL Server supportati|  
|--------------------------|------------------------------------|  
|date|Data|  
|Decimal|Decimal<br /><br /> FLOAT<br /><br /> money<br /><br /> NUMERIC<br /><br /> REAL<br /><br /> SMALLMONEY|  
|Valore intero|BIGINT<br /><br /> INT<br /><br /> smallint<br /><br /> TINYINT|  
|String|char<br /><br /> NCHAR<br /><br /> NVARCHAR<br /><br /> varchar|  
  
 I tipi di dati di SQL Server restanti non sono supportati in DQS. Per altre informazioni sui tipi di dati di SQL Server, vedere [Tipi di dati &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
##  <a name="SSIS"></a> Tipi di dati di SSIS supportati  
 Nella seguente tabella vengono fornite informazioni sui tipi di dati supportati in SSIS per ogni tipo di dati del dominio DQS:  
  
|Tipo di dati del dominio DQS.|Tipo di dati di SSIS supportati|  
|--------------------------|------------------------------|  
|date|DT_DATE|  
|Decimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Valore intero|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|String|DT_STR<br /><br /> DT_WSTR|  
  
 I tipi di dati di SSIS restanti non sono supportati in DQS. Per ulteriori informazioni su tutti i tipi di dati di SSIS, vedere [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di un dominio](../data-quality-services/managing-a-domain.md)  
  
  
