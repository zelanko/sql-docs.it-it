---
title: Impostazioni progetto (Mapping di tipo) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8a695217909641c737b7780fc4f8b80b2cb08152
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299125"
---
# <a name="project-settings-type-mapping-accesstosql"></a>Impostazioni progetto (Mapping di tipo) (AccessToSQL)
Le impostazioni di progetto del mapping dei tipi consentono di impostare i mapping dei tipi predefiniti per il progetto SSMA. È anche possibile specificare i mapping dei tipi per singoli oggetti di database. Per altre informazioni, vedere [Mapping tipi di origine e destinazione dati](mapping-source-and-target-data-types-accesstosql.md).  
  
Mapping dei tipi è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo:  
  
-   Usare la **impostazioni del progetto** finestra di dialogo per impostare le opzioni di configurazione per il progetto corrente. Per accedere alle impostazioni di mapping di tipo, nel **degli strumenti** dal menu **le impostazioni del progetto**e quindi fare clic su **Mapping dei tipi** nel riquadro sinistro.  
  
-   Usare la **impostazioni di progetto predefinite** finestra di dialogo per impostare le opzioni di configurazione per tutti i progetti. Per accedere alle impostazioni di mapping di tipo, nel **degli strumenti** dal menu **impostazioni di progetto predefinite**, selezionare tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati / modificato da  **Versione di destinazione della migrazione** elenco a discesa e quindi fare clic su **Mapping di tipo** nel riquadro sinistro.  
  
## <a name="options"></a>Opzioni  
**Tipo origine**  
Il tipo di dati di accesso per eseguire il mapping.  
  
**Tipo di destinazione**  
La destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tipo di dati di SQL Azure per il tipo di dati di accesso specificato.  
  
La tabella seguente illustra il mapping predefinito tra i tipi di dati di origine e di destinazione.  
  
|Tipo di dati di accesso|Tipo di dati di SQL Server|  
|--------------------|------------------------|  
|**binary[\*..\*]**|**varbinary[\*]**|  
|**boolean**|**bit**|  
|**byte**|**tinyint**|  
|**currency**|**money**|  
|**data**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**guid**|**uniqueidentifier**|  
|**integer**|**smallint**|  
|**long**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**memo**|**nvarchar(max)**|  
|**Memo** - per Access 97|**ntext**|  
|**single**|**real**|  
|**text[\*..\*]**|**nvarchar[\*]**|  
|**testo [\*.. \*]** - per Access 97|**varchar[\*]**|  
  
**Aggiungi**  
Fare clic per aggiungere un tipo di dati all'elenco di mapping.  
  
**Modifica**  
Fare clic per modificare un tipo di dati nell'elenco di mapping.  
  
**Rimuovi**  
Fare clic per rimuovere il mapping dei tipi di dati selezionato dall'elenco di mapping.  
  
**Ripristina predefiniti**  
Fare clic per reimpostare tutti i mapping dei tipi di dati per le impostazioni predefinite SSMA.  
  
## <a name="see-also"></a>Vedere anche  
[Mapping dei tipi di dati origine e destinazione](mapping-source-and-target-data-types-accesstosql.md)  
[Reference(Access) dell'interfaccia utente](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
