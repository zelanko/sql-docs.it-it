---
title: Abilitare Resource Governor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, enabling
ms.assetid: 4d17af53-cf11-4ce4-aab4-deda94a49836
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7b1b0f780457aa5a4d26cbb463c9f31a94185f0d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063580"
---
# <a name="enable-resource-governor"></a>Abilitare Resource Governor
  Resource Governor è disabilitato per impostazione predefinita. È possibile abilitare Resource Governor tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o Transact-SQL.  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#LimitationsRestrictions), [Autorizzazioni](#Permissions)  
  
-   **Per attivare Resource Governor usando:**  [Esplora oggetti](#RGOnObjEx), [le proprietà di Resource Governor](#RGOnProp), [Transact-SQL](#RGOnTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
 L'abilitazione di Resource Governor determina i risultati riportati di seguito:  
  
-   Viene eseguita la funzione di classificazione per le nuove connessioni, in modo che i relativi carichi di lavoro possano essere assegnati ai gruppi del carico di lavoro.  
  
-   Vengono imposti e applicati i limiti delle risorse specificati nella configurazione di Resource Governor.  
  
-   Le richieste esistenti prima dell'abilitazione di Resource Governor sono interessate dalle modifiche alla configurazione effettuate quando Resource Governor è stato disabilitato.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 Non è possibile utilizzare l'istruzione `ALTER RESOURCE GOVERNOR` per abilitare Resource Governor quando in una transazione utente.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per abilitare Resource Governor è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="enable-resource-governor-using-object-explorer"></a><a name="RGOnObjEx"></a> Abilitare Resource Governor utilizzando Esplora oggetti  
 **Per abilitare Resource Governor utilizzando Esplora oggetti**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire Esplora oggetti ed espandere in modo ricorsivo il nodo **Gestione** fino a **Resource Governor**.  
  
2.  Fare clic con il pulsante destro del mouse su **Resource Governor**, quindi su **Abilita**.  
  
##  <a name="enable-resource-governor-using-resource-governor-properties"></a><a name="RGOnProp"></a> Abilitare Resource Governor utilizzando Proprietà di Resource Governor  
 **Per abilitare Resource Governor utilizzando la pagina Proprietà di Resource Governor**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire Esplora oggetti ed espandere in modo ricorsivo il nodo **Gestione** fino a **Resource Governor**.  
  
2.  Fare clic con il pulsante destro del mouse su **Resource Governor** , quindi fare clic su **Proprietà**. In questo modo viene aperta la pagina **Proprietà di Resource Governor** .  
  
3.  Fare clic sulla casella di controllo **Abilita Resource Governor** , quindi scegliere **OK**.  
  
##  <a name="enable-resource-governor-using-transact-sql"></a><a name="RGOnTSQL"></a> Abilitare Resource Governor utilizzando Transact-SQL  
 **Per abilitare Resource Governor utilizzando Transact-SQL**  
  
1.  Eseguire l'istruzione **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Esempio (Transact-SQL)  
 Nell'esempio seguente viene abilitato Resource Governor.  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Resource Governor](resource-governor.md)   
 [Disabilitare Resource Governor](disable-resource-governor.md)   
 [Pool di risorse di Resource Governor](resource-governor-resource-pool.md)   
 [Gruppo di carico di lavoro di Resource Governor](resource-governor-workload-group.md)   
 [Funzione di classificazione di Resource Governor](resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
