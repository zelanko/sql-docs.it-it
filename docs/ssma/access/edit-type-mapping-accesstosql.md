---
title: Modificare il mapping dei tipi (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7f9d9530-6c04-41d9-bbe7-d91820a30066
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7d41fc2f01e2cfbc2b20c58ea9be640f2afd8ea0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006578"
---
# <a name="edit-type-mapping-accesstosql"></a>Modificare il mapping dei tipi (AccessToSQL)
Il **modifica del mapping dei tipi** nella finestra di dialogo consente di specificare la modalità di mapping dei tipi tra gli oggetti di database di origine e destinazione.  
  
È possibile accedere a questa finestra di dialogo in diverse posizioni:  
  
-   Quando si seleziona un database di origine o di un oggetto di database, il **Mapping dei tipi** verrà visualizzata la scheda a destra della finestra di esplorazione di metadati. Fare clic su **Add** per aggiungere un nuovo mapping dei tipi, o fare clic su **modificare** per modificare un mapping di tipo esistente.  
  
-   Nel **Tools** dal menu **le impostazioni del progetto** o **impostazioni di progetto predefinite**. Nella finestra di dialogo visualizzata, selezionare **Mapping dei tipi**. Fare clic su **Add** per aggiungere un nuovo mapping dei tipi, o fare clic su **modificare** per modificare un mapping di tipo esistente.  
  
Mapping dei tipi di tabella specifiche di eseguire l'override del database e i mapping dei tipi di progetto. Mapping di specifiche del database di eseguire l'override dei mapping di progetto.  
  
## <a name="options"></a>Opzioni  
**Tipo di origine**  
Selezionare il tipo di dati di origine eseguire il mapping a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati.  
  
Se il tipo di dati è di lunghezza variabile, i campi seguenti verranno visualizzati sotto **tipo di origine**:  
  
**From**  
Specificare la lunghezza minima per questo mapping. Ad esempio, per il **testo** tipo di dati, è possibile immettere 10 per specificare che questo mapping è per un intervallo di partire **text(10)** .  
  
**To**  
Specificare la lunghezza massima consentita per questo mapping. Ad esempio, per il **testo** tipo di dati, è possibile immettere 20 per specificare che questo mapping è per un intervallo termina **text(20)** .  
  
**Tipo di destinazione**  
Selezionare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati a cui viene eseguito il mapping al tipo di origine. Quando SSMA consente di creare la tabella o una stored procedure in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il tipo di dati di origine verrà modificato in questo tipo di dati.  
  
Se il tipo di dati è di lunghezza variabile, il campo seguente verrà visualizzato nella **tipo di destinazione**:  
  
**Replace with**  
Specificare la lunghezza di destinazione per questo mapping. Ad esempio, per il **nvarchar** tipo di dati, è possibile immettere per specificare che il tipo di dati di origine specificato deve essere mappato a 20 **nvarchar(20)** .  
  
