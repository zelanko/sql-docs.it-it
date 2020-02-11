---
title: Corrispondenza nomi (creazione guidata vista origine dati) (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourceviewwizard.namematchingcriteria.f1
ms.assetid: 7f811e02-0fe6-45c9-a7b7-29c61032d96b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 866bdea710033a0cfa3bdadb34282c96c810d730
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072400"
---
# <a name="name-matching-data-source-view-wizard-analysis-services"></a>Corrispondenza nomi (Configurazione guidata vista origine dati) (Analysis Services)
  Utilizzare la pagina **Corrispondenza nomi** per selezionare il criterio da utilizzare per il rilevamento delle possibili relazioni esistenti tra le tabelle selezionate per la vista origine dati e le altre tabelle dello schema. Se non esistono relazioni fisiche di chiave esterna tra le tabelle, questo criterio consente all'utente di identificare e aggiungere tabelle correlate alla vista origine dati. Anche le relazioni logiche identificate mediante la corrispondenza dei nomi vengono aggiunte alla vista origine dati.  
  
> [!NOTE]  
>  Questa pagina viene visualizzata solo se si seleziona un'origine dei dati che dispone di più tabelle ma non di relazioni di chiave esterna tra una delle tabelle.  
  
## <a name="options"></a>Opzioni  
 **Crea relazioni logiche individuando le corrispondenze tra le colonne**  
 Selezionare questa opzione per utilizzare un criterio di corrispondenza dei nomi che consenta di rilevare le possibili dipendenze e relazioni logiche esistenti tra le tabelle che si desidera includere nella vista origine dati e le altre tabelle dello schema. Se questa casella di controllo viene deselezionata, non viene utilizzato alcun criterio di corrispondenza dei nomi per identificare le relazioni logiche esistenti tra le tabelle dell'origine dei dati.  
  
 **Corrispondenze chiavi esterne**  
 Consente di selezionare il criterio da utilizzare per la creazione di relazioni logiche tra le tabelle e le viste dell'origine dei dati. I caratteri non alfanumerici contenuti nelle stringhe di corrispondenza vengono ignorati. Ad esempio, le stringhe "Customer ID", "Customer_ID" e "CustomerID" corrispondono. Selezionare una delle opzioni riportate nella tabella seguente per creare relazioni in base alle condizioni specificate.  
  
|Select|Per creare|  
|------------|---------------|  
|**Stesso nome della chiave primaria**|Una relazione logica a qualsiasi tabella che dispone di un nome di colonna che corrisponde alla colonna chiave primaria nella tabella selezionata.|  
|**Stesso nome della tabella di destinazione**|Una relazione logica a qualsiasi tabella che dispone di un nome di colonna che corrisponde al nome di una tabella selezionata.|  
|**Nome tabella di destinazione + nome chiave primaria**|Una relazione logica a qualsiasi tabella in cui un nome di colonna corrisponde al nome della tabella selezionata concatenato al nome della colonna chiave primaria per la tabella selezionata,in base a tale ordine. I caratteri non alfanumerici inclusi nella concatenazione vengono ignorati. Ad esempio, le stringhe "Product ID", "Product_ID" e "ProductID" corrispondono.|  
  
 **Descrizione ed esempio**  
 Consente di visualizzare una descrizione e un esempio del criterio selezionato.  
  
  
