---
title: Generale (progettazione Database) (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.databasedesigner.dbconfigurationpane.f1
helpviewer_keywords:
- Database Designer
ms.assetid: 00c9c42b-db2b-4620-8fb6-1e165ff0cbdd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a353d633287ad4b535a88b9ba76fa403a20c9e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731057"
---
# <a name="general-database-designer-analysis-services---multidimensional-data"></a>Generale (Progettazione database) (Analysis Services - Dati multidimensionali)
  Utilizzare la scheda **Generale** per modificare le proprietà di un database di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 **Per visualizzare la scheda Generale**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire un progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
2.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse sul progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , fare clic su **Modifica database**e quindi fare clic sulla scheda **Generale** .  
  
## <a name="basic-options"></a>Opzioni standard  
 Espandere la sezione **Standard** per modificare le informazioni di base relative al database. In questa sezione sono incluse le opzioni seguenti:  
  
 **Nome database**  
 Consente di visualizzare il nome del database.  
  
> [!NOTE]  
>  Per rinominare il database, in **Esplora soluzioni**fare clic con il pulsante destro del mouse sul progetto e quindi scegliere **Proprietà**. Nella finestra di dialogo **Pagine delle proprietà** del database, nella pagina **Distribuzione** modificare il valore della proprietà **Database** digitando il nome desiderato.  
  
 **Descrizione**  
 Consente di digitare una descrizione del database.  
  
## <a name="translations-options"></a>Opzioni relative alle traduzioni  
 Espandere la sezione **Traduzioni** per creare e modificare le traduzioni della didascalia e della descrizione del database. Nella griglia visualizzata in questa sezione sono incluse le colonne seguenti:  
  
 **Lingua**  
 Consente di selezionare la lingua per la transazione specificata.  
  
 Per aggiungere una nuova traduzione alla griglia, fare clic su  **\<Aggiungi nuova traduzione >**.  
  
 **Didascalia tradotta**  
 Consente di digitare la didascalia del database nella lingua della traduzione. Se vuota, viene utilizzata la didascalia predefinita del database.  
  
 **Descrizione tradotta**  
 Consente di digitare la descrizione del database nella lingua della traduzione. Se vuota, viene utilizzata la descrizione predefinita del database.  
  
## <a name="account-type-mapping-options"></a>Opzioni relative al mapping dei tipi di conto  
 Espandere la sezione **Mapping tipi di conto** per modificare la funzione di aggregazione predefinita associata a ogni **tipo** di conto nel database selezionato.  
  
> [!NOTE]  
>  Questa opzione si applica esclusivamente ai cubi nei quali una o più misure usano la funzione di aggregazione *ByAccount* .  
  
 Nella griglia visualizzata in questa sezione sono incluse le colonne seguenti:  
  
 **Name**  
 Consente di digitare il nome del tipo di conto.  
  
 Per aggiungere un nuovo tipo di account, fare clic su  **\<Aggiungi nuovo tipo di conto >**.  
  
 **Alias**  
 Consente di impostare il nome predefinito del tipo di conto per l'utilizzo con Configurazione guidata funzionalità di Business Intelligence. Se la colonna è lasciata vuota, viene utilizzato il valore predefinito indicato nella colonna **Nome** .  
  
 **Funzione di aggregazione**  
 Consente di selezionare la funzione di aggregazione da utilizzare per il tipo di conto selezionato.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [I database modello multidimensionale &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)   
 [Gli avvisi di &#40;finestra di progettazione del Database&#41; &#40;Analysis Services - dati multidimensionali&#41;](warnings-database-designer-analysis-services-multidimensional-data.md)  
  
  
