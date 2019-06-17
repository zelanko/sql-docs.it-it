---
title: Impostazioni (migrazione) (AccessToSQL) del progetto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Migration settings
- Project Settings dialog box, Migration
ms.assetid: 4caebc9c-8680-4b99-a8fa-89c43161c95d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 441366208d2bfd886794dd7e50dca7e0aef7b3ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299285"
---
# <a name="project-settings-migration-accesstosql"></a>Impostazioni progetto (migrazione) (AccessToSQL)
Le impostazioni del progetto di migrazione consentono di configurare la modalità di migrazione dati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
Nel riquadro di migrazione è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo.  
  
-   Usare la **impostazioni del progetto** finestra di dialogo per impostare le opzioni di configurazione per il progetto corrente. Per accedere a impostazioni di migrazione, scegliere il **degli strumenti** dal menu **le impostazioni del progetto**, fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi fare clic su  **Migrazione**.  
  
-   Usare la **impostazioni di progetto predefinite** finestra di dialogo per impostare le opzioni di configurazione per tutti i progetti. Per accedere a impostazioni di migrazione, scegliere il **degli strumenti** dal menu **impostazioni di progetto predefinite**, selezionare il tipo di progetto in **versione di destinazione della migrazione** casella combinata dei quali è Per accedere alle impostazioni, scegliere **generali** nella parte inferiore del riquadro a sinistra e quindi fare clic su **migrazione**.  
  
## <a name="options"></a>Opzioni  
**Vincoli CHECK**  
Specifica se SSMA deve verificare i vincoli durante l'aggiunta di dati alle tabelle.  
  
-   **Modalità predefinita**: False  
  
-   **La modalità ottimistico**: True  
  
-   **Modalità intero**: False  
  
**Attive trigger**  
Specifica se SSMA deve attivare i trigger di inserimento quando aggiunge dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelle.  
  
-   **Modalità predefinita**: False  
  
-   **La modalità ottimistico**: True  
  
-   **Modalità intero**: False  
  
**Mantieni valori Identity**  
Specifica se SSMA consente di mantenere i valori di identità di accesso durante l'aggiunta di dati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se questo valore è False, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assegna i valori identity.  
  
-   **Modalità predefinita**: True  
  
-   **La modalità ottimistico**: True  
  
-   **Modalità intero**: False  
  
**Mantieni valori Null**  
Specifica se SSMA consente di mantenere i valori null nei dati di origine durante l'aggiunta di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], indipendentemente dal fatto che i valori predefiniti specificati nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Modalità predefinita**: True  
  
-   **La modalità ottimistico**: False  
  
-   **Modalità intero**: True  
  
**Blocchi di tabella**  
Specifica se SSMA consente di bloccare le tabelle durante l'aggiunta di dati alle tabelle durante la migrazione dei dati. Se il valore è False, SSMA Usa blocchi di riga.  
  
-   **Modalità predefinita**: True  
  
-   **La modalità ottimistico**: True  
  
-   **Modalità intero**: True  
  
**Sostituire le date non supportate**  
Specifica se le date di accesso precedenti alla meno recente dovrebbe risolversi da SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datetime data (01 gennaio 1753).  
  
-   Per mantenere i valori di data corrente, selezionare **non eseguono alcuna operazione**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non accetta le date precedenti 01 gennaio 1753 in una colonna datetime. Se si usano le date precedenti, è necessario convertire i valori datetime ai valori di carattere.  
  
-   Per convertire le date precedenti 01 gennaio 1753 su NULL, selezionare **sostituire con un valore NULL**.  
  
-   Per sostituire le date precedenti 01 gennaio 1753 con una data supportata, selezionare **sostituire con più vicino data supportati**. Se si seleziona questo valore, per impostazione predefinita più vicino data supportati venga selezionata come 01 gennaio 1753.  
  
**Dimensioni del batch**  
Dimensioni batch utilizzate durante la migrazione dei dati. Una transazione viene registrata dopo ogni batch. Per impostazione predefinita, le dimensioni del batch per tutti gli schemi sono 10000.  
  
## <a name="see-also"></a>Vedere anche  
[Reference(Access) dell'interfaccia utente](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
