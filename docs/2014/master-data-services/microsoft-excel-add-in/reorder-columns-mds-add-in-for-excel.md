---
title: Riordinare le colonne (componente aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ac00462e-c0f7-4b8d-86f2-d9eda2598a15
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7d14023208ddb9cac2eb5c2f3c3c2770f2363dc7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478911"
---
# <a name="reorder-columns-mds-add-in-for-excel"></a>Riordinare le colonne (componente aggiuntivo MDS per Excel)
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]è possibile riordinare le colonne filtrando l'elenco prima del caricamento.  
  
 Quando si riordinano gli attributi nella finestra di dialogo **Filtro** , i dati vengono caricati in Excel con il nuovo ordine. Tuttavia, quando si filtrano i dati dell'attributo la volta successiva, verrà ripristinato l'ordine della progettazione originale. Per modificare l'ordine in modo permanente, è consigliabile che un amministratore modifichi l'ordine nell'area **Amministrazione sistema** di Gestione dati master. Per altre informazioni, vedere [Change the Order of Attributes](../change-the-order-of-attributes.md).  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Esplora** .  
  
### <a name="to-reorder-mds-managed-columns"></a>Per riordinare le colonne gestite da MDS  
  
1.  Aprire Excel e nella scheda **Dati master** connettersi a un repository MDS. Per altre informazioni, vedere [Connettersi a un repository MDS &#40;componente aggiuntivo MDS per Excel&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  Nel riquadro **Esplora dati master** selezionare un modello e una versione. L'elenco di entità viene popolato.  
  
    -   Se il riquadro **Esplora dati master** non è visibile, nel gruppo **Connetti e carica** fare clic su **Esplora dati master**.  
  
    -   Se il riquadro **Esplora dati master** è disabilitato, significa che il foglio esistente contiene già i dati gestiti da MDS. Per abilitare il riquadro, aprire un nuovo foglio di lavoro.  
  
3.  Nel riquadro **Esplora dati master** , fare clic su un'entità.  
  
4.  Nel gruppo **Connetti e carica** fare clic su **Filtro**.  
  
5.  Nella finestra di dialogo **Filtro** , nella sezione **Colonne** , nell'elenco di attributi fare clic sull'attributo che si desidera spostare.  
  
6.  A destra dell'elenco, fare clic sulla freccia **SU** o **GIÙ** per spostare l'attributo a sinistra o a destra nel foglio di lavoro.  
  
7.  Ripetere il passaggio 7 per ogni attributo fino a che l'ordine dall'alto in basso rappresenta l'ordine da sinistra a destra che si desidera nel foglio di lavoro.  
  
8.  Fare clic su **Carica dati**. Il foglio viene popolato con dati gestiti da MDS e le colonne vengono visualizzate nell'ordine specificato.  
  
## <a name="see-also"></a>Vedere anche  
 [Il caricamento dei dati &#40;componente aggiuntivo MDS per Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
