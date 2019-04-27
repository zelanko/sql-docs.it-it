---
title: Formato dei pacchetti SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: cfe0e5dc-5be3-4222-b721-fe83665edd94
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b7288952ce9b57b0825f20d1a93fcbcd20d3c37
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766324"
---
# <a name="ssis-package-format"></a>Formato del pacchetto SSIS
  Nella versione corrente di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]sono state apportate modifiche significative al formato dei pacchetti (file DTSX) per semplificare la lettura del formato e il confronto dei pacchetti. È inoltre possibile unire in modo più affidabile i pacchetti che non contengono modifiche in conflitto o modifiche archiviate in formato binario.  
  
 Per visualizzare il formato di file di pacchetto DTSX corrente, vedere [ \[MS-DTSX\]: Specifica di formato di File XML del pacchetto Data Transformation Services](https://go.microsoft.com/fwlink/?LinkId=233251).  
  
 Nell'elenco seguente vengono indicate le modifiche al formato del file. Per visualizzare gli esempi di codice di queste modifiche, vedere la pagina relativa alle [modifiche al formato del pacchetto in SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=233255).  
  
-   Sono state applicate convenzioni di formattazione per semplificare la lettura e la comprensione del file DTSX.  
  
-   Il formato è più conciso. Gli elementi separati per ogni proprietà sono stati resi persistenti come gli attributi, ad eccezione di PackageFormatVersion. Gli attributi sono elencati in ordine alfabetico e le proprietà con valori predefiniti non sono più persistenti. Infine, gli elementi che possono essere visualizzati più volte, sono ora contenuti all'interno di un elemento padre.  
  
-   La maggior parte degli oggetti all'interno di un pacchetto che può fare riferimento ad altri oggetti contiene ora un attributo `refId` definito nel pacchetto XML. Anziché rendere persistente gli ID di derivazione, ora è stato reso persistente `refID`. Gli ID di derivazione vengono ancora utilizzati all'interno del runtime e vengono rigenerati al caricamento del pacchetto.  
  
     Il valore `refId` è una stringa univoca leggibile e comprensibile, rispetto ai valori GUID o ai valori integer. La stringa è simile ai valori del percorso utilizzati per le configurazioni del pacchetto nelle versioni precedenti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
     Se si uniscono le modifiche tra due versioni di un pacchetto, `refId` può essere utilizzato nelle operazioni di ricerca e sostituzione per verificare che tutti i riferimenti all'oggetto siano stati aggiornati correttamente.  
  
-   Le informazioni sul layout sono contenute in una sezione CData.  
  
-   Le annotazioni sono persistenti in testo non crittografato. In questo modo è più facile estrarre le informazioni per la generazione automatica della documentazione.  
  
  
