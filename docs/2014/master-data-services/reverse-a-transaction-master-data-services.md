---
title: Invertire una transazione (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], reversing
ms.assetid: 6f7c3f07-0f64-4283-8c9c-93facd00a046
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1bc306eda0d7c12bfbb6d7fc32e50189b213c30b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971101"
---
# <a name="reverse-a-transaction-master-data-services"></a>Invertire una transazione (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]gli amministratori possono invertire una transazione quando è necessario annullare un'azione. Esempi di transazioni sono modifiche al valore dell'attributo, spostamenti di gerarchie o eliminazioni di membri.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   È necessario avere l'autorizzazione per accedere all'area funzionale **Gestione versioni** .  
  
-   È necessario essere un amministratore del modello. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-reverse-a-transaction"></a>Per invertire una transazione  
  
1.  Scegliere [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Gestione versioni **dalla home page di**.  
  
2.  Sulla barra dei menu fare clic su **Transazioni**.  
  
3.  Nella pagina **Transazioni** selezionare un modello dall'elenco **Modello** .  
  
4.  Selezionare una versione dall'elenco **Versione** .  
  
5.  Fare clic sulla riga nella griglia per la transazione che si desidera invertire.  
  
6.  Fare clic su **Inverti transazione selezionata**.  
  
7.  Nella finestra di dialogo di conferma fare clic su **OK**. Un'altra transazione viene aggiunta alla griglia per registrare la transazione invertita.  
  
## <a name="see-also"></a>Vedere anche  
 [Transazioni &#40;Master Data Services&#41;](../../2014/master-data-services/transactions-master-data-services.md)   
 [Riattivare un membro o una raccolta &#40;Master Data Services&#41;](../../2014/master-data-services/reactivate-a-member-or-collection-master-data-services.md)  
  
  
