---
title: Impostare i parametri per la finestra di dialogo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.parameter.f1
ms.assetid: fac02b6d-d247-447a-8940-e8700c7ac350
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7d60820ba7c384347aeeec80d8c41f934078eca8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056869"
---
# <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
  La finestra di dialogo **Imposta parametri** consente di associare un parametro nuovo o esistente a una proprietà di un'attività. È possibile aprire la finestra di dialogo facendo clic con il pulsante destro del mouse su un'attività o sulla scheda Flusso di controllo in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)], quindi selezionando **Imposta parametri**. Nell'elenco seguente vengono descritti gli elementi dell'interfaccia utente della finestra di dialogo. Per altre informazioni sui parametri, vedere [Parametri di Integration Services &#40;SSIS&#41;](integration-services-ssis-package-and-project-parameters.md).  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Proprietà**  
 Selezionare la proprietà dell'attività che si desidera associare a un parametro. Questo elenco viene popolato con tutte le proprietà che è possibile impostare come parametri.  
  
 **Usa parametro esistente**  
 Selezionare questa opzione per associare la proprietà dell'attività a un parametro esistente, quindi selezionare il parametro dall'elenco a discesa.  
  
 **Non utilizzare il parametro**  
 Selezionare questa opzione per rimuovere un riferimento a un parametro. Il parametro non viene eliminato.  
  
 **Crea nuovo parametro**  
 Selezionare questa opzione per creare un nuovo parametro che si desidera associare alla proprietà dell'attività.  
  
 **Name**  
 Specificare il nome del parametro che si desidera creare.  
  
 **Descrizione**  
 Specificare la descrizione per il parametro.  
  
 **Valore**  
 Specificare il valore predefinito per il parametro. Definito anche valore predefinito per la progettazione, potrà essere sostituito in seguito in fase di distribuzione.  
  
 **Ambito**  
 Specificare l'ambito del parametro selezionando l'opzione **Progetto** o **Pacchetto**. I parametri del progetto vengono utilizzati per fornire input esterno ricevuto dal progetto a uno o più pacchetti nel progetto. I parametri del pacchetto consentono di modificare l'esecuzione del pacchetto senza doverlo modificare e ridistribuire.  
  
 **Sensibile**  
 Specificare se il parametro è sensibile selezionando o deselezionando la casella di controllo. I valori di parametri sensibili sono crittografati nel catalogo e risultano NULL quando vengono visualizzati con Transact-SQL o con SQL Server Management Studio.  
  
 **Obbligatorio**  
 Specificare se il parametro richiede che un valore diverso dal valore predefinito per la progettazione venga specificato prima dell'esecuzione del pacchetto.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
  
