---
description: Apportare modifiche alle tabelle selezionate per l'acquisizione di modifiche
title: Apportare modifiche alle tabelle selezionate per l'acquisizione di modifiche | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- makChanToTab
ms.assetid: a309f82a-c6ef-464d-a6ef-df555bfb609a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b6caa3f5d6d1abe5a8d4a197391da18a74942f00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88394487"
---
# <a name="make-changes-to-the-tables-selected-for-capturing-changes"></a>Apportare modifiche alle tabelle selezionate per l'acquisizione di modifiche

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  In questa finestra di dialogo è possibile selezionare colonne specifiche della tabella selezionata da cui acquisire le modifiche. È anche possibile modificare le informazioni **Security Role** e **Capture Instance** .  
  
 È possibile apportare le modifiche seguenti alle tabelle selezionate per l'acquisizione delle modifiche in questa finestra di dialogo.  
  
 **Cambiare le colonne incluse nell'istanza di CDC:**  
  
 Eseguire una o entrambe le operazioni seguenti:  
  
-   Selezionare la casella di controllo accanto a eventuali colonne aggiuntive che si desidera includere.  
  
-   Deselezionare la casella di controllo accanto alle colonne che non si desidera più includere.  
  
 **Modificare il tipo di dati per una colonna specifica**:  
  
 È possibile selezionare un tipo di dati diverso per una colonna specifica. È possibile solo modificare il tipo di dati su un tipo di dati compatibile con il tipo di dati originale.  
  
 Per modificare il tipo di dati, fare clic nella colonna **Tipo di dati** e selezionare un tipo di dati diverso. Sono disponibili solo i tipi di dati compatibili con il tipo di dati originale.  
  
> [!NOTE]  
>  Se non è possibile selezionare tipi di dati aggiuntivi, l'elenco a discesa non è disponibile.  
  
 **Modificare il ruolo di sicurezza**  
  
 Digitare un nuovo nome oppure modificare il nome esistente del ruolo di sicurezza nel campo **Ruolo di sicurezza** .  
  
 **Modificare o aggiungere un'istanza di acquisizione**  
  
 Nel campo **Istanza di acquisizione** immettere un nome per l'istanza di acquisizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di creazione dell'istanza del database delle modifiche di SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Selezionare tabelle e colonne Oracle](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
