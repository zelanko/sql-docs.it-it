---
title: Modificare il mapping dei tipi (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 513f071a-d5e6-4ed5-acca-269bf76323c5
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: cd8dfbd7aa4205424c45861f6ada1113f76d344e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029167"
---
# <a name="edit-type-mapping-sybasetosql"></a>Modificare il mapping dei tipi (SybaseToSQL)
La finestra di dialogo **Modifica mapping tipi** consente di specificare la modalità di mapping dei tipi tra gli oggetti di database di origine e di destinazione.  
  
È possibile accedere a questa finestra di dialogo in diverse posizioni:  
  
-   Quando si seleziona un database di origine o un oggetto di database, la scheda **mapping dei tipi** viene visualizzata a destra di Esplora metadati. Fare clic su **Aggiungi** per aggiungere un nuovo mapping dei tipi oppure fare clic su **modifica** per modificare un mapping dei tipi esistente.  
  
-   Scegliere **Impostazioni progetto** o **Impostazioni progetto predefinite**dal menu **strumenti** . Nella finestra di dialogo risultante selezionare **mapping dei tipi**. Fare clic su **Aggiungi** per aggiungere un nuovo mapping dei tipi oppure fare clic su **modifica** per modificare un mapping dei tipi esistente.  
  
I mapping dei tipi specifici della tabella sostituiscono i mapping dei tipi di progetto e di database. I mapping specifici del database sostituiscono i mapping del progetto.  
  
## <a name="options"></a>Opzioni  
**Tipo di origine**  
Consente di selezionare il tipo di dati di origine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il mapping a un tipo di dati.  
  
Se il tipo di dati è di lunghezza variabile, i campi seguenti verranno visualizzati in **tipo di origine**:  
  
**From**  
Consente di specificare la lunghezza minima per questo mapping. Per il tipo di dati **nchar** , ad esempio, è possibile immettere 10 per specificare che il mapping è relativo a un intervallo a partire da **nchar (10)**.  
  
**A**  
Consente di specificare la lunghezza massima consentita per questo mapping. Per il tipo di dati **nchar** , ad esempio, è possibile immettere 20 per specificare che il mapping è per un intervallo che termina con **nchar (20)**.  
  
**Tipo di destinazione**  
Consente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionare il tipo di dati a cui viene eseguito il mapping del tipo di dati di origine. Quando SSMA crea la tabella o stored procedure in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il tipo di dati di origine verrà modificato in questo tipo di dati.  
  
Se il tipo di dati è di lunghezza variabile, il campo seguente verrà visualizzato in **tipo di destinazione**:  
  
**Replace with**  
Specificare la lunghezza di destinazione per questo mapping. Per il tipo di dati **nvarchar** , ad esempio, è possibile immettere 20 per specificare che il tipo di dati di origine specificato deve essere mappato a **nvarchar (20)**.  
  
