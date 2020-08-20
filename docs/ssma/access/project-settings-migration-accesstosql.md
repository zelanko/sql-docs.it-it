---
description: Impostazioni progetto (migrazione) (AccessToSQL)
title: Impostazioni progetto (migrazione) (AccessToSQL) | Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 94bd5cc9a8cb0db9079db981ec50a5fa6af7b20c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480530"
---
# <a name="project-settings-migration-accesstosql"></a>Impostazioni progetto (migrazione) (AccessToSQL)
Le impostazioni del progetto di migrazione consentono di configurare il modo in cui viene eseguita la migrazione dei dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
Il riquadro migrazione è disponibile nelle finestre di dialogo **Impostazioni progetto** e **Impostazioni progetto predefinite** .  
  
-   Utilizzare la finestra di dialogo **Impostazioni progetto** per impostare le opzioni di configurazione per il progetto corrente. Per accedere alle impostazioni di migrazione, scegliere **Impostazioni progetto**dal menu **strumenti** , fare clic su **generale** nella parte inferiore del riquadro sinistro, quindi fare clic su **migrazione**.  
  
-   Utilizzare la finestra di dialogo **Impostazioni progetto predefinite** per impostare le opzioni di configurazione per tutti i progetti. Per accedere alle impostazioni di migrazione, nel menu **strumenti** selezionare **Impostazioni progetto predefinite**, selezionare il tipo di progetto nella casella combinata **versione destinazione migrazione** di cui si desidera accedere alle impostazioni, fare clic su **generale** nella parte inferiore del riquadro sinistro, quindi fare clic su **migrazione**.  
  
## <a name="options"></a>Opzioni  
**Vincoli CHECK**  
Specifica se SSMA deve verificare i vincoli quando aggiunge dati alle tabelle.  
  
-   **Modalità predefinita**: false  
  
-   **Modalità ottimistica**: true  
  
-   **Modalità completa**: false  
  
**Attive trigger**  
Specifica se SSMA deve attivare i trigger di inserimento quando aggiunge dati alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelle.  
  
-   **Modalità predefinita**: false  
  
-   **Modalità ottimistica**: true  
  
-   **Modalità completa**: false  
  
**Mantieni valori Identity**  
Specifica se SSMA conserva i valori Identity di accesso quando aggiunge dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se questo valore è false, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assegna i valori Identity.  
  
-   **Modalità predefinita**: true  
  
-   **Modalità ottimistica**: true  
  
-   **Modalità completa**: false  
  
**Mantieni valori Null**  
Specifica se SSMA conserva i valori null nei dati di origine quando aggiunge dati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , indipendentemente dai valori predefiniti specificati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Modalità predefinita**: true  
  
-   **Modalità ottimistica**: false  
  
-   **Modalità completa**: true  
  
**Blocchi di tabella**  
Specifica se SSMA blocca le tabelle quando aggiunge dati alle tabelle durante la migrazione dei dati. Se il valore è false, SSMA utilizza i blocchi di riga.  
  
-   **Modalità predefinita**: true  
  
-   **Modalità ottimistica**: true  
  
-   **Modalità completa**: true  
  
**Sostituisci date non supportate**  
Specifica se SSMA deve correggere le date di accesso precedenti alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data DateTime più recente (01 gennaio 1753).  
  
-   Per memorizzare i valori correnti della data, selezionare **non eseguire alcuna operazione**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non accetterà le date precedenti al 01 gennaio 1753 in una colonna DateTime. Se si utilizzano date precedenti, è necessario convertire i valori DateTime in valori di tipo carattere.  
  
-   Per convertire le date precedenti al 01 gennaio 1753 in NULL, selezionare **Sostituisci con null**.  
  
-   Per sostituire le date precedenti al 01 gennaio 1753 con una data supportata, selezionare **Sostituisci con la data più vicina supportata**. Se si seleziona questo valore, per impostazione predefinita la data più vicina supportata verrà selezionata come 01 gennaio 1753.  
  
**Dimensioni dei batch**  
Dimensioni batch utilizzate durante la migrazione dei dati. Una transazione viene registrata dopo ogni batch. Per impostazione predefinita, le dimensioni del batch per tutti gli schemi sono pari a 10000.  
  
## <a name="see-also"></a>Vedere anche  
[Guida di riferimento all'interfaccia utente (accesso)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
