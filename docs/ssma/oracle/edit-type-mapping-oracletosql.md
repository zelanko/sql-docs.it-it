---
title: Modificare il mapping dei tipi (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7078b4ed-c779-4bf3-8db8-f9dcb3edd50f
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: ee8d2e4c16987f5cc012f734cdf649cde7f4ebb8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63288579"
---
# <a name="edit-type-mapping-oracletosql"></a>Modificare il mapping dei tipi (OracleToSQL)
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
Specificare la lunghezza minima per questo mapping. Ad esempio, per il **nchar** tipo di dati, è possibile immettere 10 per specificare che questo mapping è per un intervallo di partire **nchar (10)**.  
  
**Per**  
Specificare la lunghezza massima consentita per questo mapping. Ad esempio, per il **nchar** tipo di dati, è possibile immettere 20 per specificare che questo mapping è per un intervallo termina **nchar(20)**.  
  
**Tipo di destinazione**  
Selezionare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati a cui viene eseguito il mapping al tipo di origine. Quando SSMA consente di creare la tabella o una stored procedure in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il tipo di dati di origine verrà modificato in questo tipo di dati.  
  
Se il tipo di dati è di lunghezza variabile, il campo seguente verrà visualizzato nella **tipo di destinazione**:  
  
**Replace with**  
Specificare la lunghezza di destinazione per questo mapping. Ad esempio, per il **nvarchar** tipo di dati, è possibile immettere per specificare che il tipo di dati di origine specificato deve essere mappato a 20 **nvarchar(20)**.  
  
