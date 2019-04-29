---
title: Applicare le regole di business (componente aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2722e678de98bbfbf5a1181a69101fbe2a9427d8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62923955"
---
# <a name="apply-business-rules-mds-add-in-for-excel"></a>Applicare le regole business (componente aggiuntivo MDS per Excel)
  Nel [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] applicare le regole di business quando si vuole convalidare i dati e confermare che sono validi. È possibile correggere le convalide e pubblicare nuovamente i dati.  
  
> [!NOTE]  
>  La convalida dei dati si verifica automaticamente quando si pubblicano dati. Per altre informazioni, vedere [Stored procedure di convalida &#40;Master Data Services&#41;](../validation-stored-procedure-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'accesso all'area funzionale **Visualizzatore** .  
  
-   È necessario avere un foglio di lavoro attivo che contenga i dati gestiti da MDS.  
  
### <a name="to-apply-business-rules"></a>Per applicare le regole business  
  
1.  Nel gruppo **Pubblica e convalida** fare clic su **Applica regole**.  
  
    > [!NOTE]  
    >  Il numero di membri (righe) convalidati contemporaneamente dipende da un'impostazione in [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]. Per altre informazioni, vedere [Impostazioni delle regole business](../system-settings-master-data-services.md#BusinessRules).  
  
2.  I dati vengono convalidati automaticamente rispetto alle regole business e vengono visualizzate due colonne. Se queste colonne non sono visualizzate automaticamente, nel gruppo **Pubblica e convalida** fare clic su **Mostra stato** per visualizzarle.  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicazione di dati &#40;componente aggiuntivo MDS per Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
