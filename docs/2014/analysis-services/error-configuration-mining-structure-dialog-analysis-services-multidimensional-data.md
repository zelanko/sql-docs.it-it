---
title: Configurazione errori (finestra di dialogo struttura di Data Mining) (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.miningstructuredialog.general.f1
ms.assetid: d9aa028b-bad9-49c7-a81c-c2150e4dd481
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e8973d9dd6fb5d96afc9cf66ded4b894f0dfe6df
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081364"
---
# <a name="error-configuration-mining-structure-dialog-box-analysis-services---multidimensional-data"></a>Configurazione errori (finestra di dialogo Struttura di data mining) (Analysis Services - Dati multidimensionali)
  La pagina **Configurazione errori** della finestra di dialogo **Proprietà struttura di data mining** in **SQL Server Management Studio** consente di impostare le proprietà di configurazione degli errori di una struttura di data mining in un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="options"></a>Opzioni  
 **Usa configurazione errori predefinita**  
 Selezionare questa opzione per utilizzare la configurazione errori predefinita per gli oggetti nell'operazione di elaborazione.  
  
 **Azione per errore chiave**  
 Consente di scegliere una delle azioni seguenti da eseguire quando viene rilevata una nuova chiave che non può essere ricercata durante l'elaborazione:  
  
-   **Converti in sconosciuta** aggrega le informazioni relative al record nel membro sconosciuto.  
  
-   **Scarta record** esclude le informazioni relative al record dall'elaborazione dell'oggetto.  
  
 **Ignora conteggio errori**  
 Fare clic su questa opzione per ignorare qualsiasi eventuale errore che si verifichi durante l'elaborazione.  
  
 **Arresta in caso di errore**  
 Fare clic su questa opzione per arrestare l'elaborazione in caso di errori. Questa opzione implica l'attivazione delle impostazioni **Numero di errori** e **Azione in caso di errore** .  
  
 **Numero di errori**  
 Consente di immettere il numero di errori che verranno ignorati prima di arrestare l'elaborazione.  
  
 **Azione in caso di errore**  
 Consente di scegliere una delle azioni seguenti da eseguire se il numero di errori supera il valore impostato in **Numero di errori**:  
  
-   **Arresta elaborazione** termina l'operazione di elaborazione.  
  
-   **Arresta registrazione** arresta la registrazione degli errori senza però interrompere l'elaborazione.  
  
 **Chiave non trovata**  
 Specificare una delle azioni seguenti da eseguire quando non viene trovata una chiave durante l'elaborazione di un oggetto:  
  
-   **Ignora errore** ignora l'errore  
  
-   **Segnala e continua** segnala l'errore e continua l'operazione di elaborazione.  
  
-   **Segnala e arresta** segnala l'errore e arresta l'operazione di elaborazione.  
  
 **Chiave duplicata**  
 Specificare una delle azioni seguenti da eseguire se viene trovata una chiave duplicata durante l'elaborazione di un oggetto:  
  
-   **Ignora errore** ignora l'errore  
  
-   **Segnala e continua** segnala l'errore e continua l'operazione di elaborazione.  
  
-   **Segnala e arresta** segnala l'errore e arresta l'operazione di elaborazione.  
  
 **Chiave Null convertita in sconosciuta**  
 Consente di specificare una delle azioni seguenti da eseguire quando viene aggiunta una chiave membro Null al membro sconosciuto durante l'elaborazione di un oggetto.  
  
-   **Ignora errore** ignora l'errore  
  
-   **Segnala e continua** segnala l'errore e continua l'operazione di elaborazione.  
  
-   **Segnala e arresta** segnala l'errore e arresta l'operazione di elaborazione.  
  
 **Chiave Null non consentita**  
 Consente di specificare una delle azioni seguenti da eseguire quando viene trovata una chiave Null non consentita durante l'elaborazione di un oggetto.  
  
-   **Ignora errore** ignora l'errore  
  
-   **Segnala e continua** segnala l'errore e continua l'operazione di elaborazione.  
  
-   **Segnala e arresta** segnala l'errore e arresta l'operazione di elaborazione.  
  
 **Percorso log degli errori**  
 Consente di digitare il percorso completo e il nome del file di log degli errori.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Proprietà struttura di data mining &#40;Analysis Services - Data Mining&#41;](mining-structure-properties-dialog-analysis-services-data-mining.md)   
 [Generale &#40;finestra di dialogo struttura di Data Mining&#41; &#40;Analysis Services - Data Mining&#41;](general-mining-structure-dialog-box-analysis-services-data-mining.md)  
  
  
