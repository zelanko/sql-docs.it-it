---
title: Editor ciclo foreach (pagina Mapping variabili) | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.mapping.f1
ms.assetid: aa847b87-f391-48a5-9849-eeda2d6b00b9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03488e4cfd3a0cc905a58166f381f68eb3292c49
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058528"
---
# <a name="foreach-loop-editor-variable-mappings-page"></a>Editor ciclo Foreach (pagina Mapping variabili)
  Utilizzare la pagina **Mapping variabili** della finestra di dialogo **Editor ciclo Foreach** per eseguire il mapping delle variabili al valore della raccolta. Il valore della variabile viene aggiornato con i valori della raccolta in ogni iterazione del ciclo.  
  
 Per informazioni sull'utilizzo del contenitore Ciclo Foreach in un pacchetto di Integration Services, vedere [Foreach Loop Container](control-flow/foreach-loop-container.md) . Per informazioni su come configurarlo, vedere [Configurazione di un contenitore Ciclo Foreach](../../2014/integration-services/configure-a-foreach-loop-container.md).  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Nell' [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] esercitazione relativa alla creazione di un pacchetto ETL semplice è inclusa una lezione in cui viene illustrato come aggiungere e configurare un ciclo foreach.  
  
## <a name="options"></a>Opzioni  
 **Variabile**  
 Selezionare una variabile esistente oppure fare clic su \<**Nuova variabile**> per creare una nuova variabile.  
  
> [!NOTE]  
>  Dopo aver eseguito il mapping di una variabile, viene aggiunta automaticamente una nuova riga all'elenco di **variabili** .  
  
 **Argomenti correlati**: [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md)  
  
 **Indice**  
 Se si utilizza l'enumeratore Foreach Item, specificare l'indice della colonna nel valore della raccolta di cui eseguire il mapping alla variabile. Per altri tipi di enumeratore, l'indice è di sola lettura.  
  
> [!NOTE]  
>  L'indice è in base 0.  
  
 **Argomenti correlati**: eseguire [un ciclo su file e tabelle di Excel utilizzando un contenitore ciclo foreach](control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
 **Elimina**  
 Selezionare una variabile e quindi fare clic su **Elimina**.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor ciclo foreach &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor ciclo foreach &#40;pagina raccolta&#41;](../../2014/integration-services/foreach-loop-editor-collection-page.md)   
 [Pagina Espressioni](expressions/expressions-page.md)   
 [Contenitore Ciclo For](control-flow/for-loop-container.md)  
  
  
